# Authentifizierung über OpenID Connect

`OpenID Connect 1.0` ist eine Authentifizierungsschicht basierend auf dem `OAuth 2.0`-Protokoll. Sie ermöglicht es den Clients, die Identität des Endbenutzers auf REST-ähnliche Weise von einem Authentifizierungs-Anbieter zu erhalten.

Goobi workflow kann als `OpenID Connect Client` fungieren und konfiguriert werden. Bei der Implementierung wurde besonders darauf geachtet, dass möglichst jeder `OpenID Connect` Anbieter angesprochen werden kann. Aus diesem Grund sind die Einstellungen in der `goobi_config.properties` relativ komplex:

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

Außerdem muss noch der `login` endpoint in der API freigeschaltet werden. Dazu wird ein neuer Eintrag in der `goobi_rest.xml` angelegt:

{% code title="goobi_rest.xml" %}
```xml
<endpoint path="/login/openid">
    <method name="post">
        <allow />
    </method>
</endpoint>
```
{% endcode %}

Mit diesen Einstellungen wird ein Nutzer beim ersten Besuch von Goobi workflow auf die Seite des Authentifizierungs-Providers weitergeleitet. Dort ist der Nutzer entweder schon eingeloggt und wird direkt wieder zu Goobi workflow zurück weitergeleitet oder er muss sich zunächst einloggen und wird daraufhin weitergeleitet zu Goobi workflow.

Nach der Durchführung der Weiterleitung des Nutzers überprüft Goobi die Antwort des Authentifizierungs-Providers auf Validität und sucht nach einem Nutzer mit einer `SSO-ID`, die mit dem `email`-Claim aus der OpenID Connect Antwort übereinstimmt. Kann ein Nutzer gefunden werden, wird dieser anschließend eingeloggt.