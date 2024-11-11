# Best Practice für die Entwicklung von Goobi und für die Arbeit mit Eclipse

## 1.4.1 Sinnvolle Softwarepakete
Um mit den Repositories und dem Quellcode sinnvoll arbeiten zu können, sollten weitere Pakete installiert werden. Diese haben sich als sinnvoll erwiesen:

### Linux

```bash
sudo apt install git
sudo apt install maven
```

### Mac

```bash
brew install git
brew install maven
```


## 1.4.2 Timeout für Tomcat vermeiden
Unter Umständen dauert der Start des Tomcat länger als der per default gesetzte Timeout. Daher kann es sinnvoll sein, diesen anzupassen. Dies kann innerhalb des `Servers View` erfolgen. Dazu müssen die Einstellungen per Doppelklick auf den erzeugen Server `goobi` geöffnet werden, so dass dann im obereren rechten Bereich der Konfiguration im Bereich `Timeouts` ein anderer Wert für den Start des Tomcat Servers angegeben werden kann.

![Timeout](screen.png)


## 1.4.3 Tomcat von Persistenz bzw. Serialisierung abhalten
Um die Fehlermeldungen von Tomcat zu Unterbinden, wenn die Serialisierung der Sessions nicht funktioniert, kann man folgendermaßen vorgehen:
  - in Eclipse das Projekt `Servers` öffnen
  - darin für den richtigen Tomcat die Datei `context.xml` öffnen
  - innerhalb der Datei den folgenden Block so ändern und speichern:
  
```xml
<!-- Uncomment this to disable session persistence across Tomcat restarts -->
<Manager pathname="" />
```

## 1.4.4 HotSwap Agent (JRebel Ersatz)
​Der HotSwap Agent ermöglicht es, dass Dateien bearbeitet und im laufenden Betrieb automatisiert aktualisiert werden können. Dies funktioniert insbesondere für java- und xhtml-Code in Goobi Workflow und zugehörigen Plugins.

Mit einem erfolgreich eingerichteten HotSwap Agent müssen Dateien später nur noch in ihrem lokalen Repository geändert und gespeichert werden und die Änderungen sind direkt beim Neuladen einer Seite im Webbrowser präsent.


### Allgemeines
- Die offizielle Webseite des HotSwap Agenten ist hier: [http://hotswapagent.org/](http://hotswapagent.org/ "Offizielle Webseite des HotSwap Agenten")
- Tomcat **MUSS** im `DEBUG` Modus gestartet werden, sonst funktioniert das class-reloading nicht. In Eclipse ist dies das Icon mit dem Käfer statt dem normalen Run-Button.
- Falls Tomcat nur zum Teil hochfährt und dann stehen bleibt, kann es sein, dass irgendwo Breakpoints gesetzt sind. Diese können in Eclipse mit `Run` -> `Skip All Breakpoints` übersprungen oder mit `Run` -> `Remove All Breakpoints` entfernt werden.


### Installation
- Herunterladen der passenden HotSwap-JVM (Java 11) von hier: [https://github.com/TravaOpenJDK/trava-jdk-11-dcevm/releases](https://github.com/TravaOpenJDK/trava-jdk-11-dcevm/releases "Link zur HotSwap-JVM")
- Heruntergeladenes HotSwap-JDK entpacken und in Eclipse in den Preferences als JRE bekannt machen
- Details des WTP-Tomcat konfigurieren, durch Doppelklick auf den Server im Server-View
  - Klick auf `Runtime Environment`, um dort das bekannt gemachte HotSwap JDK als `JRE` auszuwählen
  - Klick auf `Open launch configuration`, um dort dieses VM-Argument hinzufügen: `-XX:HotswapAgent=fatjar`
  - Unter `Publishing` die Option `Never publish automatically` auswählen
  - Auf dem Reiter `Modules` den Parameter `auto-reload` auf `false` setzen (bzw. in der server.xml im richtigen Bereich so setzen: `reloadable="false"`) **Hinweis:** der Reiter befindet sich am unteren Rand des Server-Bearbeitungs-Views.


### Konfiguration
- Vor der Inbetriebnahme muss noch eine Konfigurationsdatei mit dem Namen `hotswap-agent.properties` innerhalb des Goobi Source Ordners liegen:

```bash
nano ~/git/goobi-workflow/Goobi/src/hotswap-agent.properties
```
​
Detailierte Informationen zur Konfiguration befinden sich hier: [http://hotswapagent.org/mydoc_configuration.html](http://hotswapagent.org/mydoc_configuration.html "Seite mit detailierten Informationen zur Konfiguration")

- Darin muss sich ein Inhalt wie der folgende befinden (Wichtig: komplette Pfade, keine Tilde für Home-Verzeichnis):

```bash
extraClasspath=/home/PETER/git/goobi-workflow/Goobi/webapp/WEB-INF/classes/; \
/home/PETER/git/goobi-plugin-administration-snippet-creator/plugin/target/classes; \
/home/PETER/git/goobi-plugin-opac-json/goobi-plugin-opac-json/target/classes; \
/home/PETER/git/goobi-plugin-workflow-aeon-process-creation/plugin/target/classes;

webappDir=/home/PETER/git/goobi-workflow/Goobi/webapp; \
/home/PETER/git/goobi-plugin-administration-snippet-creator/plugin/src/main/resources/GUI/META-INF/resources; \
/home/PETER/git/goobi-plugin-opac-json/goobi-plugin-opac-json/src/main/resources/GUI/META-INF/resources; \
/home/PETER/git/goobi-plugin-workflow-aeon-process-creation/plugin/src/main/resources/GUI/META-INF/resources;
```

### Besonderheit bei Plugins
- Wenn Plugins mit berücksichtigt werden sollen, müssen diese innerhalb der Konfigurationsdatei explizit benannt sein (so wie hier in der Beispielkonfiguration sichtbar)
- Plugins müssen vor dem Goobi-Start in kompilierter Form in die typischen Plugin-Ordner kopiert werden (also z.B. nach `/opt/digiverso/goobi/plugins/workflow/` und `/opt/digiverso/goobi/plugins/GUI/`)
- gelesen und ausgeführt werden die Plugins dann aus dem Eclipse-Repository
- Es müssen keine xhtml-Dateien der Plugins mehr im Goobi-uii-Ordner liegen