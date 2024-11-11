# Authentifizierung über HTTP-Header

Die HTTP-Header Authentifizierung liest einen HTTP-Header in der Anfrage aus, und überprüft ob es einen Nutzer gibt, bei dem die `SSO-ID` mit dem Inhalt des Headers übereinstimmt. Sollte es den Nutzer geben, wird er eingeloggt. Da HTTP-Header sehr leicht gesetzt werden können, sollte diese Authentifizierung nur benutzt werden, wenn Goobi workflow nur über einen vorgelagerten Webserver (zum Beispiel `Apache2` oder `nginx`) erreichbar ist, und dieser die eigentliche Authentifizierung übernimmt. Um diese Authentifizierung zu nutzen, müssen in der Konfigurationsdatei `goobi_config.properties` folgende Schalter gesetzt sein:

```bash
EnableHeaderLogin=true
SsoHeaderName=ssoid
showSSOLogoutPage=true
```

Dabei wird mittels `EnableHeaderLogin` die Funktionalität eingeschaltet, mit dem Parameter `SsoHeaderName` wird der Name des auszulesenden Headers festgelegt. `showSSOLogoutPage` sorgt dafür, dass beim Logout eine Zwischenseite angezeigt und der Nutzer nicht direkt wieder neu eingeloggt wird.

Außerdem muss noch der `login` endpoint in der API freigeschaltet werden. Dazu wird ein neuer Eintrag in der `goobi_rest.xml` angelegt:

{% code title="goobi_rest.xml" %}
```xml
<endpoint path="/login/header">
    <method name="get">
        <allow />
    </method>
</endpoint>
```
{% endcode %}

## Beispielkonfiguration für CAS mittels Apache2

Eine Beispiel-Einrichtung mit einem `Apache2` Webserver und `CAS single sign on` könnte folgendermaßen durchgeführt werden:

Zuerst müssen `Apache2` und das `CAS-Modul` installiert werden.

```bash
apt install apache2 libapache2-mod-auth-cas libcurl4 libpcre3
```

Das `CAS-Modul` setzt voraus, dass einige Verzeichnisse existieren und der `Apache2`-Prozess auf diese Verzeichnisse Zugriff hat:

```bash
mkdir -p /var/cache/httpd/mod_auth_cas/ && chown daemon /var/cache/httpd/mod_auth_cas/
```

Abschließend muss noch die Konfiguration für den Webserver `Apache2` angepasst werden, damit das Modul geladen und der richtige `upstream-Header` gesetzt wird:

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
  CASAuthNHeader ssoid
  require valid-user
</Location>
```

## Beispielkonfiguration für SAML mittels Apache2 und mod_auth_melon

Diese Beispiel-Einrichtung nutzt `mod_auth_melon`, um eine Authentifizierung mittels SAML Diensten und dem Goobi workflow header login umzusetzen. Hierbei nutzen wir für unseren neu einzurichtenden service provider die entityID `https://mygoobi.tld/mygoobisp/` und nehmen an, dass unser Server unter der Domain `mygoobi.tld` zu erreichen ist. Das abzusichernde Goobi ist dann unter der URL `https://mygoobi.tld/goobi/` zu erreichen.

Als erstes sollten Apache2 und `mod_auth_melon` installiert werden:

```bash
apt install apache2 libapache2-mod-auth-mellon
```

Als nächstes sollten die Service Provider Metadaten mitsamt des privaten Schlüssel und des Zertifikats erzeugt werden. Dazu gibt es im mod auth mellon repository ein praktisches Script:

[https://github.com/latchset/mod_auth_mellon/blob/master/mellon_create_metadata.sh](https://github.com/latchset/mod_auth_mellon/blob/master/mellon_create_metadata.sh)

Dieses Script erwartet zwei Parameter, die entityID unseres service provider, sowie die URL unter der die SAML endpoints des Service Provider erreicht werden können:

```bash
./mellon_create_metadata.sh "https://mygoobi.tld/mygoobisp/" "https://mygoobi.tld/mellon"
```

Der Befehl erzeugt einen privaten Schlüssel, ein Zertifikat sowie die Metadaten für den service provider.

In der Apache2 Konfiguration muss nun das auth-Modul geladen werden, sowie zwei `Location`s angelegt werden:

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

Die erste `Location` ist die globale `mellon` Konfiguration, in der wir die Metadaten für den identity provider und den service provider konfigurieren. Die zweite `Location` ist die zu schützende Goobi-Anwendung. Hier konfigurieren wir den `Authtype` zu `Mellon` und verlangen nach einem validen Nutzer. Goobi workflow nutzt dann wie oben beschrieben den `ssoid` header, um Nutzer zu identifizieren.