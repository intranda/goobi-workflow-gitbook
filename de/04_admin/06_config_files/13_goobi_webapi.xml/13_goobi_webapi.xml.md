# goobi_webapi.xml

Mit der Konfigurationsdatei `goobi_webapi.xml` werden bestimmte API Endpunkte des Goobi Workflow Servers für andere Server oder Clients freigeschaltet. Die Datei befindet sich üblicherweise an folgendem Speicherpfad:

```bash
/opt/digiverso/goobi/config/goobi_webapi.xml
```

Beispielhaft sieht diese Konfigurationsdatei wie folgt aus:

{% code title="goobi_webapi.xml" %}
```xml
<?xml version="1.0"?>
<config_webapi>
  <credentials ip="0:0:0:0:0:0:0:1" password="CHANGEME">
    <command name="closeStep"/>
    <command name="addToProcessLog"/>
    <command name="setErrorStep"/>
    <command name="help"/>
  </credentials>
  <credentials ip="127.0.0.1" password="CHANGEME">
    <command name="closeStep"/>
    <command name="addToProcessLog"/>
    <command name="setErrorStep"/>
    <command name="help"/>
  </credentials>
  <credentials ip="10.20.30.40" password="super_admin_password">
    <command name="/"/>
  </credentials>
  <credentials ip="20.40.60.80" password="admin_password">
    <command name="/process"/>
  </credentials>
  <credentials ip="40.60.80.100" password="user_password">
    <command name="/process/check"/>
  </credentials>
</config_webapi>
```
{% endcode %}

Goobi Workflow stellt eine REST-API zur Verfügung, bei der zwischen dem Goobi Workflow Server und anderen Netzwerkteilnehmern mittels HTTPS Protokoll und JSON Datenobjekten kommuniziert wird.

Die Funktionen, die mit der API ausgeführt werden, sind als Endpunkte in der URL angegeben. Zum Beispiel gibt folgende URL die Details eines Vorgangs mit der angegebenen ID `MY_ID` zurück:

```text
http://goobi.your-domain.org/Goobi/api/process/details/id/MY_ID?token=test
```

Es gibt allerdings auch Befehle wie `process/create` oder `process/delete`, die nur von bestimmten Nutzern ausgeführt werden dürfen.

Ein `Nutzer` kann ein anderer Server oder Client sein. In beiden Fällen braucht er eine feste IP-Adresse, für die der Zugriff freigeschaltet wird.

Für jedes Zugriffsrecht wird ein `<credentials>` Element verwendet. Der `ip` Parameter beinhaltet entweder die IPv4-Adresse oder die IPv6-Adresse des Nutzers. Mit dem `password` Parameter wird ein Token angegeben, das in einer Anfrage von der jeweiligen Nutzer-IP-Adresse als URL-Parameter angegeben werden muss. Ist zum Beispiel in der Zugriffsregel für die IP-Adresse `ip="10.20.30.40"` das Token `password="super_user_password"` angegeben, so kann eine API-Anfrage nur beantwortet werden, wenn der Nutzer mit der IPv4-Adresse `10.20.30.40` den URL-Parameter `token=super_user_password` verwendet.

Das Token sollte keine Sonderzeichen oder URL-Syntax Zeichen beinhalten. Andernfalls müssen diese entsprechend der URL-Spezifikation später in der Anfrage codiert werden. Ist in der Zugriffsregel das Token `My Password` angegeben, so muss das Leerzeichen in der Anfrage-URL durch den Hexadezimalwert `0x20` ersetzt werden und der URL-Parameter sieht wie folgt aus: `token=My%20Password`.

{% hint style="info" %}
**Hinweis:** Da Goobi das HTTPS-Protokoll verwendet, wird die Anfrage verschlüsselt übertragen und das Token kann nicht von Dritten ausgelesen werden.
{% endhint %}

Jede Zugriffsregel beinhaltet einen oder mehrere API-Befehle. Diese Befehle oder Befehlsgruppen können verwendet werden, sobald die oben beschriebene Kombination von IP-Adresse und Token übereinstimmt. Ein Befehl wird mit dem `<command>` Element definiert und hat genau einen Parameter `name`, der den Befehl beinhaltet. Der Befehl selbst kann optional mit einem Schrägstrich (`/`) beginnen.

Im obigen Beispiel sind drei Zugriffsregeln angegeben, die die unterschiedlichen Zugriffsrechte für verschiedene Anwendergruppen definieren. So hat ein Superadministrator die Möglichkeit, alle API-Befehle (`/`) zu benutzen. Ein normaler Administrator kann alle Unterbefehle von `process` ausführen. Für einen Standardnutzer ist nur der Befehl `process/check` freigeschaltet.