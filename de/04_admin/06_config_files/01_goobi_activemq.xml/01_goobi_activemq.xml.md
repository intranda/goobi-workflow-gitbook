# goobi_activemq.xml

In der Konfigurationsdatei `goobi_activemq.xml` werden die Einstellungen für die von Goobi Workflow verwendete Java-Bibliothek `org.apache.activemq` angegeben.

Goobi Workflow verwendet die Datei nicht selbst, sondern gibt sie direkt als Konfiguration an die Bibliothek weiter. Diese Dokumentation stellt nur die wichtigsten Einstellungen dar, die für Goobi eine Rolle spielen. Eine ausführlichere Dokumentation ist auf der Webseite von activemq zu finden.

Die Datei befindet sich üblicherweise an folgendem Speicherpfad:

```bash
/opt/digiverso/goobi/config/goobi_activemq.xml
```

Beispielhaft sieht diese Konfigurationsdatei wie folgt aus:

{% code title="goobi_activemq.xml" %}
```xml
<beans
    xmlns="http://www.springframework.org/schema/beans"
    xmlns:amq="http://activemq.apache.org/schema/core"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
    http://activemq.apache.org/schema/core http://activemq.apache.org/schema/core/activemq-core.xsd">
    <broker xmlns="http://activemq.apache.org/schema/core" brokerName="localhost" schedulerSupport="true" schedulerDirectory="/opt/digiverso/goobi/activemq/scheduler">
        <transportConnectors>
            <transportConnector name="stomp" uri="stomp://localhost:61613" />
            <transportConnector name="tcp" uri="tcp://localhost:61616" />
        </transportConnectors>
        <persistenceAdapter>
            <kahaDB directory="/opt/digiverso/goobi/activemq/messages" journalMaxFileLength="32mb" />
        </persistenceAdapter>
        <systemUsage>
            <systemUsage>
                <memoryUsage>
                    <memoryUsage limit="64 mb"/>
                </memoryUsage>
                <storeUsage>
                    <storeUsage limit="512 mb"/>
                </storeUsage>
                <tempUsage>
                    <tempUsage limit="128 mb"/>
                </tempUsage>
            </systemUsage>
        </systemUsage>
        <managementContext>
            <managementContext createConnector="false"/>
        </managementContext>
        <plugins>
            <redeliveryPlugin fallbackToDeadLetter="true"
                sendToDlqIfMaxRetriesExceeded="true">
                <redeliveryPolicyMap>
                    <redeliveryPolicyMap>
                        <redeliveryPolicyEntries>
                            <redeliveryPolicy queue="goobi_fast"
                                maximumRedeliveries="5"
                                initialRedeliveryDelay="10000"
                                backOffMultiplier="1.5"
                                useExponentialBackOff="true"/>
                        </redeliveryPolicyEntries>
                        <defaultEntry>
                            <!-- the fallback policy for all other destinations -->
                            <redeliveryPolicy maximumRedeliveries="10"
                                initialRedeliveryDelay="300000"
                                backOffMultiplier="1.5"
                                useExponentialBackOff="true"/>
                        </defaultEntry>
                    </redeliveryPolicyMap>
                </redeliveryPolicyMap>
            </redeliveryPlugin>
            <simpleAuthenticationPlugin>
                <users>
                    <authenticationUser username="goobi" password="goobi"
                        groups="admins,publishers,consumers"/>
                    <authenticationUser username="worker" password="worker"
                        groups="consumers"/>
                </users>
            </simpleAuthenticationPlugin>
            <authorizationPlugin>
                <map>
                    <authorizationMap>
                        <authorizationEntries>
                            <authorizationEntry topic=">" read="admins" write="admins" admin="admins" />
                            <authorizationEntry queue=">" read="admins" write="admins" admin="admins" />
                            <authorizationEntry queue="goobi_fast" read="consumers" write="publishers" admin="publishers" />
                            <authorizationEntry queue="goobi_slow" read="consumers" write="publishers" admin="publishers" />
                            <authorizationEntry queue="goobi_status" read="admins" write="consumers" />
                        </authorizationEntries>
                    </authorizationMap>
                </map>
            </authorizationPlugin>
        </plugins>
    </broker>
</beans>
```
{% endcode %}

## Verwendete XML-Namensräume

Diese Konfigurationsdatei kann in komplexeren Anwendungen mehrere XML-Namensräume verwenden.

Das Wurzelelement `<beans>` verwendet immer diesen Standard-Namensraum:

```xml
xmlns="http://www.springframework.org/schema/beans"
```

Das Unterelement `<broker>` verwendet immer diesen Standard-Namensraum:

```xml
xmlns="http://activemq.apache.org/schema/core"
```

## Einstellungen für den Message Broker

Alle Einstellungen, die für die Nutzung des Message Brokers von Goobi Workflow wichtig sind, werden innerhalb des `<broker>`-Elements vorgenommen.

Mit dem Parameter `brokerName` wird der Name des Message Brokers angegeben. Da dies der einzige auf localhost (auf diesem Computersystem) ist, ist der Name standardmäßig `localhost`.

Der Parameter `schedulerSupport` gibt an, ob ein Scheduler für Multithreading eingesetzt wird.

Mit dem Parameter `schedulerDirectory` wird ein vollständiger Dateipfad zu einem ausführbaren Scheduler angegeben.

### Freischalten von URIs mit bestimmten Protokollen

Mit dem Element `<transportConnectors>` wird eine Liste von freigeschalteten Endpunkten mitsamt den verwendbaren Protokollen angegeben. Jedes darin enthaltene `<transportConnector>` Element gibt einen Endpunkt an.

Ein Endpunkt hat üblicherweise zwei Parameter. Mit dem `name`-Parameter wird ein Name für die Freischaltung festgelegt. Dies kann zum Beispiel der Name des Protokolls sein. Der `uri` Parameter gibt einen Uniform Resource Identifier an, der aus einem Protokoll, einer IP-Adresse oder Domain, einer Portnummer, einem Pfad und eventuellen Parametern besteht. Von der hier angegebenen URL kann später mit dem angegebenen Port und dem entsprechenden Protokoll auf activemq zugegriffen werden.

### Verwendete Datenbank

Es kann vorkommen, dass übertragene Informationen nicht direkt vom Empfänger angenommen werden. Wen diese lange genug nicht abgefragt werden, speichert activemq sie in einer eigenen Datenbank. Diese wird mit dem Element `<persistenceAdapter>` konfiguriert.

Standardmäßig wird die `kahaDB` verwendet, daher beinhaltet die Konfiguration ein Element `<kahaDB>` mit dem Parameter `directory`, in dem der vollständige Dateipfad zur Datenbank angegeben wird.

Zusätzlich kann der Parameter `journalMaxFileLength` angegeben werden, um die Dateigröße in der Datenbank zu begrenzen. Dabei wird eine der Maßeinheiten `mb` oder `gb` verwendet.

### Speicherbegrenzung

Mit dem Element `<systemUsage>` kann der zur Verfügung stehende Speicherplatz für die übertragenen Daten in der Warteschlange begrenzt werden.

Das Element `<memoryUsage>` definiert die maximale Größe von verwendetem Arbeitsspeicher.

Das Element `<storeUsage>` definiert die maximale Größe der internen Datenbank.

Das Element `<tempUsage>` definiert die maximale Größe von temporären Dateien.

Die üblichsten Maßeinheiten für den `limit`-Parameter sind `mb` und `gb`.

### Eigene Verbindung für JMX

Mit dem Element `<managementContext>` wird üblicherweise eine eigene Verbindung für JMX (Java Management Extensions) ausgeschaltet. Der Parameter `createConnector` ist standardmäßig auf `false` gesetzt, damit die Standardverbindung verwendet wird.

### Plugins

Diese Konfiguration für den Message Broker ist standardmäßig mit drei Plugins ausgestattet, die die Authentifizierung und das Redelivery-System übernehmen.

#### Plugin für Benutzergruppen

Mit dem `<authenticationPlugin>` werden Benutzergruppen und deren Zugriffsrechte auf verschiedene Warteschlangen definiert.

Mit jedem `<authorizationEntry>` wird eine Warteschlange und die dazugehörigen Details angegeben. Dabei gibt der `queue` Parameter die verwendete Warteschlange an. Mit dem Parameter `topic` kann statt Lese- und Schreibrechten für eine Warteschlange der Zugriff auf bestimmte Themen konfiguriert werden.

Statt einem Namen kann bei einer Warteschlange oder einem Thema der Wert `>` gesetzt werden. Dies ist ein Universaloperator und trifft auf alle Warteschlangen und Themen zu.

Die Parameter `read`, `write` und `admin` geben Nutzergruppen an, die jeweils lesend, schreibend und mit Administratorberechtigung auf die jeweilige Warteschlange oder das Thema zugreifen können. Mehrere Nutzergruppen in einem Parameter können mit Komma getrennt werden.

#### Plugin für Benutzer und Passwörter

Mit dem `<simpleAuthenticationPlugin>` werden Benutzer angelegt und Passwörter sowie Benutzergruppen für Benutzer definiert. Jedes `<authenticationUser>` Element gibt dabei einen authentifizierbaren Benutzer an. Mit den Parametern `username` und `password` werden der Nutzername und das notwendige Passwort definiert, mit denen sich der Nutzer (oder eine andere Software) authentifizieren muss.

Zusätzlich gibt es den Parameter `groups`, der eine kommagetrennte Liste von Benutzergruppen beinhaltet, denen der jeweilige Benutzer angehört. Diese Gruppen sind relevant für das `<authorizationPlugin>`.

#### Plugin für die Fehlerbehandlung

Mit dem `<redeliveryPlugin>` wird eine detailiertere Fehlerbehandlung für das Neu-Senden von fehlerhaft übertragenen Daten konfiguriert. Dieses Plugin hat zwei boolsche Parameter, die das finale Speichern von mehrfach fehlgeschlagenen Übertragungsversuchen und deren Inhalten steuern.

Mit dem Parameter `fallbackToDeadLetter` werden Nachrichten ab einer bestimmten Anzahl an fehlgeschlagenen Übertragungsversuchen nicht weiter übertragen, um die Auslastung des Systems gering zu halten.

Mit dem Parameter `sendToDlqIfMaxRetriesExceeded` wird eine Nachricht, die mehrfach nicht gesendet werden konnte, in einen Restspeicher geschrieben. Dort verbleibt sie, bis sie manuell oder durch einen späteren erfolgreichen Übertragungsversuch doch noch gelesen werden kann. So wird verhindert, dass das Warteschlangensystem mit nicht funktionsfähigen Verbindungen ausgelastet wird.

In dem Unterelement `<redeliveryPolicyEntries>` werden Fehlerbehandlungsregeln aufgelistet, die jeweils auf bestimmte Warteschlangen zutreffen sollen. Dabei wird für jede dort eingetragene Regel mit dem Element `<redeliveryPolicy>` und dem Parameter `queue` die zugehörige Warteschlange definiert.

In dem Element `<defaultEntry>` wird der Standardfall definiert, der dann ausgeführt wird, wenn keine der oben genannten Regeln zutrifft. In diesem Element wird mit `<redeliveryPolicy>` genau eine Regel definiert, diese benötigt allerdings keinen `queue`-Parameter, da sie in allen übigen Fällen für alle Warteschlangen verwendet wird.

Es können einige weitere Parameter für die Regeln angegeben werden. So ist es möglich, mit dem ganzzahligen `maximumRedeliveries` Parameter die maximale Anzahl an Versuchen anzugeben, bevor eine Nachricht in den Restspeicher geschrieben wird. Mit dem ebenfalls ganzzahligen Parameter `initialRedeliveryDelay` wird die Anzahl an Millisekunden angegeben, nach der ein erneuter Sendeversuch gestartet wird.

Um das System nicht dauerhaft auszulasten, kann der zeitliche Abstand zwischen erneuten Sendeversuchen jedes Mal exponentiell erhöht werden. Dafür wird der boolsche Parameter `useExponentialBackOff` auf `true` gesetzt und mit dem Parameter `backOffMultiplier` ein Multiplikationsfaktor angegeben, mit dem der Zeitraum erhöht wird. Ist dieser zum Beispiel auf 1.5 gesetzt und der initiale Zeitraum ist auf 60 Sekunden gesetzt, so wird der nächste Sendeversuch nach 1.5 * 60 = 90 Sekunden ausgeführt. Der dritte folgt nach weiteren 1.5 * 90 = 135 Sekunden.