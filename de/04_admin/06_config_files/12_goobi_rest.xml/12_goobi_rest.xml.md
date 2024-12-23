# goobi_rest.xml

In der Konfigurationsdatei `goobi_rest.xml` werden die von Goobi Workflow verwendeten REST-API-Endpoints auf Basis des jeweiligen Pfads (als Teil der URL) freigegeben. Für jeden Endpoint können die erlaubten HTTP Methoden und verschiedene Zugangsbeschränkungen definiert werden.

Die Datei befindet sich üblicherweise hier:

```bash
/opt/digiverso/goobi/config/goobi_rest.xml
```

Eine Beispielkonfiguration könnte so aussehen:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<config>
    <endpoint path="/seterrorstep.*">
        <method name="post">
            <allow netmask="0:0:0:0:0:0:0:1/128" token="CHANGEME"/>
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
    </endpoint>
    <endpoint path="/addtoprocesslog.*">
        <method name="post">
            <allow netmask="0:0:0:0:0:0:0:1/128" token="CHANGEME"/>
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
    </endpoint>
    <endpoint path="/closestep.*">
        <method name="post">
            <allow netmask="0:0:0:0:0:0:0:1/128" token="CHANGEME"/>
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
    </endpoint>
    <endpoint path="/process/check.*">
        <method name="get">
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
    </endpoint>
    <endpoint path="/processes/search">
        <method name="get">
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
        <method name="post">
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
    </endpoint>
    <endpoint path="/vocabulary/.*">
        <cors>
            <method>GET</method>
            <origin>https://intranda.com</origin>               
        </cors>
        <method name="get">
            <allow />
        </method>
        <method name="post">
            <allow />
        </method>
    </endpoint>
    <endpoint path="/mails/disable/.*">
        <method name="get">
            <allow />
        </method>
    </endpoint>

    <!-- allow all commands just locally with the token 'test'
    <endpoint path=".*">
      <method name="post">
        <allow netmask="0:0:0:0:0:0:0:1/128" token="test"/>
        <allow netmask="127.0.0.0/8" token="test"/>
      </method>
      <method name="get">
        <allow netmask="0:0:0:0:0:0:0:1/128" token="test"/>
        <allow netmask="127.0.0.0/8" token="test"/>
      </method>
      <method name="put">
        <allow netmask="0:0:0:0:0:0:0:1/128" token="test"/>
        <allow netmask="127.0.0.0/8" token="test"/>
      </method>
    </endpoint>
    -->
</config>
```

## Allgemeiner Aufbau

Eine Konfiguration besteht aus mehreren Regeln für Endpoints. Dies sind die `<endpoint>` Elemente. Jedes Endpoint-Element benötigt ein Attribut `path`. Dieses gibt den Pfad zum entsprechenden Endpoint an und darf reguläre Ausdrücke beinhalten. Die Unterelemente von `<endpoint>` sind `<method>` oder `<cors>`Elemente.

## JWT Authentifizierung (JSON Web Token)

Ein Endpoint-Element kann zusätzlich das Attribut `jwtAuth` beinhalten und eine Authentifizierung mittels JSON Web Token erfordern. Der Default-Wert ist `false`.

```xml
<endpoint path="." jwtAuth="true">
    ...
</endpoint>
```

Ist die JWT-Authentifikation eingeschaltet und das Token ungültig, antwortet Goobi mit dem HTTP Status Code 401 (Unauthorized).

## Standardmäßig freigeschaltete Endpoints

Standardmäßig sind die folgenden Pfade ohne Zugriffsbeschränkungen freigeschaltet:

```bash
/view/object/
/view/media/
/process/image/
/messages/
/processes/\\d+?/images.*
/openapi.json
```

<!---
In dem Ausdruck für die Vorgangs-ID muss genau ein Backslash in der GUI zu sehen sein. Dieses escaped das 'd'.
-->

Der Ausdruck `\\d+?` beschreibt eine Vorgangs-ID.

Befindet sich Goobi Workflow im Entwicklungsmodus, ist standardmäßig der Endpoint `/developer/` freigeschaltet. Solange Goobi Workflow ohne Port-Freigaben am Router in einem lokalen Netzwerk entwickelt wird, ist dieser Endpoint nicht öffentlich zugänglich.

## Freischalten von API-Methoden

Für jeden API-Endpoint können eine oder mehrere erlaubte HTTP-Request-Methoden angegeben werden. Dazu wird für jede verwendete HTTP-Methode ein Unterelement `method` im entsprechenden `endpoint` eingetragen. Ein `method`-Element hat genau ein Attribut `name`. Die am häufigsten verwendeten HTTP-Methoden sind:

```text
get
head
post
put
delete
options
```

Innerhalb des `method` Elements werden mit dem Element `allow` die Zugriffsfreigaben und -beschränkungen für die jeweilige Endpoint/Method-Kombination konfiguriert. Dazu werden eine oder mehrere Freigaben wie folgt hinzugefügt:

```xml
<method name="get">
    <allow netmask="0:0:0:0:0:0:0:1/128" token="CHANGEME"/>
    <allow netmask="127.0.0.0/8" token="CHANGEME"/>
    <!--
    or for public endpoints:
    -->
    <allow />
</method>
```

Mit dem Attribut `netmask` wird eine IPv4 oder IPv6 Netzmaske angegeben und das dazugehörige Token mit dem Attribut `token`. Wenn das `token` oder das `netmask` Attribut weggelassen werden, ist der Zugriff ohne Token oder mit jeder IP-Adresse erlaubt. Wird beides weggelassen, kann von jeder IP-Adresse ohne Token auf den Endpoint zugegriffen werden. Dies kann nützlich sein, wenn ein Endpoint komplett öffentlich sein soll oder durch andere Methoden (zum Beispiel JSON web tokens) authentifiziert wird. Das Token `test` kann verwendet werden, um den Zugriff auf Endpoints außschließlich von localhost zuzulassen.

Bei der Überprüfung einer Anfrage geht Goobi nach Dokumentenreihenfolge vor und überprüft das erste `<enpoint>`/`<method>` Paar, das zur Anfrage passt. Sollte keine `<allow>`-Regel gefunden werden, die zur Anfrage passt, liefert Goobi den Statuscode `401` zurück und verweigert die Verarbeitung der Anfrage. Dies impliziert auch, dass die Reihenfolge der Regeln in dieser Konfigurationsdatei beachtet werden sollte. Wenn Goobi eine Meldung mit 401 zurückgibt, kann es daran liegen, dass ein Endpoint weiter oben zu allgemein formuliert wurde und Goobi nicht bis zu einer Regel weiter unten vorstößt, da die Verarbeitung schon aufgrund der Regel weiter oben im Dokument verweigert wird.

## HTTP Header Felder

Zusätzlich zu den Freigaben können mit dem Element `header` ein oder mehrere HTTP Header-Felder angegeben werden, die bei Anfragen mit der entsprechenden Request-Methode an dem jeweiligen Endpoint von Goobi automatisch in die Header-Felder des Antwort-Protokolls geschrieben werden. Dies kann praktisch sein, wenn der Client bzw. Browser bestimmte Meta-Informationen über das Verhalten des Endpoints bekommen soll. Dazu wird mit dem Attribut `name` das HTTP Header-Feld angegeben. Das `header`-Element kann ein oder mehrere Unterelemente `value` beinhalten und kann in der Praxis wie folgt aussehen:

```xml
<method>
    <allow />
    <header name="Content-Language">
    	<value>de-DE</value>
    	<value>en-US</value>
    </header>
</method>
```

Im HTTP-Protokoll wird dann folgendes Feld hinzugefügt:

```text
HTTP/2 200 OK
...
Content-Language: de-DE, en-US
```

## CORS (Cross Origin Requests)

Die Konfiguration ermöglicht auch das Freischalten von cross-origin Anfragen. Dazu kann innerhalb eines Endpoints ein `<cors>` Element angelegt werden, in dem die erlaubten Methoden mit `<method>` Elementen und die erlaubten origins mit `<origin>` Elementen konfiguriert werden. Wenn ein `<cors>` Element für einen Endpoint konfiguriert ist, behandelt Goobi automatisch eventuell vom Browser geschickte preflight-Requests. Die Konfiguration kann zum Beispiel wie folgt aussehen:

```xml
<endpoint path="/vocabulary/.*">
    <cors>
        <method>GET</method>
        <origin>https://intranda.com</origin>               
    </cors>
    <method name="get">
        <allow />
    </method>
    <method name="post">
        <allow />
    </method>
</endpoint>
```

Die cross-origin-Methoden können mit der HTTP Request-Methode `OPTIONS` und dem in der Konfiguration angegebenen Endpoint abgefragt werden. Wird zum Beispiel eine HTTP-Anfrage mit der folgenden Kopfzeile gesendet, listet Goobi in den HTTP-Reponse-Header-Feldern die möglichen cross-origin-Methoden auf. Bei einer `OPTIONS`-Anfrage hat die Antwort keinen Inhalt und der Status-Code ist 204 (No Content).

Anfrage:
```text
OPTIONS /vocabulary/.* HTTP/2
...
```

Antwort:
```text
HTTP/2 204 No Content
...
Access-Control-Allow-Methods: GET
Access-Control-Allow-Origin: https://intranda.com
Access-Control-Allow-Headers: origin,content-type,accept,token
...
```