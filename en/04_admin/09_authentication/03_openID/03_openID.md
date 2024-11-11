# Authentication via OpenID Connect

`OpenID Connect 1.0` is an authentication layer based on the `OAuth 2.0` protocol. It enables clients to obtain the end user's identity from an authentication provider in a REST-like manner. 

Goobi workflow can function and be configured as an `OpenID Connect Client`. During implementation, particular care was taken to ensure that as many `OpenID Connect` providers as possible can be addressed. For this reason, the settings in `goobi_config.properties` are relatively complex.

```bash
# use OpenID Connect
useOpenIdConnect=true

# set this to true and the user will be redirected automatically to the OpenID Connect login provider
OIDCAutoRedirect=true

# the authorization endpoint for OpenID Connect
OIDCAuthEndpoint=https://myopenidconnect.tld/oauth2/v2.0/authorize

# the logout endpoint
OIDCLogoutEndpoint=https://myopenidconnect.tld/oauth2/logout

# the issuer uri
OIDCIssuer=https://myopenidconnect.tld/v2.0

# The JWK set. Goobi will automatically fetch the set and verify the response from the openid server
OIDCJWKSet=https://myopenidconnect.tld/discovery/keys

# the client ID configured for Goobi in you openid connect backend
OIDCClientID=the-client-id-for-goobi

# the claim that is matched against the ssoId field in the Goobi users database
OIDCIdClaim=email

# redirect to a "you are logged out" page after logout, so you are not logged in right after logging out
showSSOLogoutPage=true
```

In addition, the `login` endpoint must be activated in the API. To do this, a new entry is created in the `goobi_rest.xml`:

{% code title="goobi_rest.xml" %}
```xml
<endpoint path="/login/openid">
    <method name="post">
        <allow />
    </method>
</endpoint>
```
{% endcode %}

With these settings, a user will be redirected to the authentication provider's page the first time they visit Goobi workflow. There, the user is either already logged in and is redirected back to Goobi workflow or he or she must first log in and is then redirected to Goobi workflow. 

Once the user has been forwarded, Goobi checks the authentication provider's reply for validity and searches for a user with an `SSO-ID` that matches the `email` claim from the OpenID Connect reply. If a user can be found, he or she is then logged in.