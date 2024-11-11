# Authentication via HTTP header

HTTP header authentication reads an HTTP header in the request and checks if there is a user whose `SSO-ID` matches the content of the header. If there is a user, he will be logged in. As HTTP headers can be set very easily, this authentication should only be used if Goobi workflow can only be accessed via an upstream web server (e.g. `Apache2` or `nginx`) and this server handles the actual authentication. To use this authentication, the following switches must be set in the `goobi_config.properties` configuration file:

```bash
EnableHeaderLogin=true
SsoHeaderName=casauthn
showSSOLogoutPage=true
```

The functionality is switched on with `EnableHeaderLogin`, the parameter `SsoHeaderName` defines the name of the header to be read out. The configuration key `showSSOLogoutPage` enables a redirect to a logout page, so the user is not logged in directly after logging out. 

In addition, the `login` endpoint must be activated in the API. To do this, a new entry is created in the `goobi_rest.xml`:

{% code title="goobi_rest.xml" %}
```xml
<endpoint path="/login/header">
    <method name="get">
        <allow />
    </method>
</endpoint>
```
{% endcode %}

## Example configuration for CAS using Apache2

An example setup with an `Apache2` web server and `CAS single sign` on could be performed as follows:

First `Apache2` and the `CAS module` must be installed.

```bash
apt install apache2 libapache2-mod-auth-cas libcurl4 libpcre3
```

The `CAS module` assumes that some directories exist and that the `Apache2` process has access to these directories:

```bash
mkdir -p /var/cache/httpd/mod_auth_cas/ && chown daemon /var/cache/httpd/mod_auth_cas/
```

Finally, the configuration for the `Apache2` web server must be adjusted so that the module is loaded and the correct `upstream header` is set:

```bash
# load the CAS module
LoadModule auth_cas_module /usr/lib/apache2/modules/mod_auth_cas.so

<IfModule unixd_module>
# configure CAS
CASCookiePath /var/cache/httpd/mod_auth_cas/
CASLoginURL https://your.cas.service.tld/cas/login
CASValidateURL https://your.cas.service.tld/cas/serviceValidate
</IfModule>

# ProxyPass to Goobi...
ProxyPass "/goobi/" "http://localhost:8080/goobi/"
ProxyPassReverse "/" "http://localhost:8080/goobi/"

# ...and protect the location with CAS
<Location /goobi/>
  Authtype CAS 
  # this is the name of the header you need to set in the Goobi configuration
  CASAuthNHeader casauthn
  require valid-user
</Location>
```

## Example configuration for SAML using Apache2 and mod_auth_melon

This example setup uses `mod_auth_melon` to implement authentication using SAML services and the Goobi workflow header login. Here we use the entityID `https://mygoobi.tld/mygoobisp/` for our new service provider to be set up and assume that our server can be reached under the domain `mygoobi.tld`. The Goobi to be secured can then be reached under the URL `https://mygoobi.tld/goobi/`.

First of all, Apache2 and `mod_auth_melon` should be installed:

```bash
apt install apache2 libapache2-mod-auth-mellon
```

Next, the service provider metadata should be generated along with the private key and certificate. There is a handy script for this in the mod auth mellon repository:

[https://github.com/latchset/mod_auth_mellon/blob/master/mellon_create_metadata.sh](https://github.com/latchset/mod_auth_mellon/blob/master/mellon_create_metadata.sh)

This script expects two parameters, the entityID of our service provider, and the URL under which the SAML endpoints of the service provider can be reached:

```bash
./mellon_create_metadata.sh "https://mygoobi.tld/mygoobisp/" "https://mygoobi.tld/mellon"
```

The command generates a private key, a certificate and the metadata for the service provider. 

In the Apache2 configuration, the auth module must now be loaded and two `Location`s must be created:

```bash
LoadModule auth_mellon_module /usr/lib/apache2/modules/mod_auth_mellon.so


# ProxyPass to Goobi...
ProxyPass "/goobi/" "http://localhost:8080/goobi/"
ProxyPassReverse "/" "http://localhost:8080/goobi/"

<Location />
    MellonEnable "info"
    MellonEndpointPath "/mellon/"
    
    # This needs to be configured in the Goobi workflow configuration as 
    # SsoHeaderName=ssoid
    MellonSetEnvNoPrefix "ssoid" "mail"

    # needs to be obtained from the identity provider
    MellonIdPMetadataFile /etc/apache2/mellon/idp-metadata.xml
    
    # the next three files were created my the 
    # mellon_create_metadata.sh script mentioned above
    MellonSPMetadataFile /etc/apache2/mellon/sp-metadata.xml
    MellonSPPrivateKeyFile /etc/apache2/mellon/sp.key
    MellonSPCertFile /etc/apache2/mellon/sp.cert
</Location>

<Location /goobi/>
    Authtype "Mellon"
    Require valid-user
    MellonEnable "auth"
</Location>
```

The first `Location` is the global `mellon` configuration where we configure the metadata for the identity provider and the service provider. The second `Location` is the Goobi application to be protected. Here we configure the `Authtype` to `Mellon` and require a valid user. Goobi workflow then uses the ssoid header to identify users as described above.