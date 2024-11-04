# Servlet Container Apache Tomcat

## **Allgemein**

Goobi ist eine webbasierte Java Applikation. Damit diese im Webbrowser aufrufbar ist, muss der Java Code übersetzt werden. Hierfür ist ein Servlet Container zuständig. Beispiele für Servlet Container sind:

_**Servlet Container**_

| Servlet Container | Projekt-URL |
| :--- | :--- |
| Apache Tomcat | [http://tomcat.apache.org/](http://tomcat.apache.org/) |
| Jetty | [http://jetty.codehaus.org/jetty/](http://jetty.codehaus.org/jetty/) |
| Resin | [http://onjava.com/pub/a/onjava/2002/09/18/resin.htm](http://onjava.com/pub/a/onjava/2002/09/18/resin.html) |

Üblicherweise wird in einem `Apache Tomcat` installiert. Dieser wird aus den Standardrepositories des Betriebssystems installiert, sofern diese die Version 7 enthalten. Ist das nicht der Fall, wird der `Apache Tomcat` von Hand installiert und gepflegt.

## **Beispiel: Ubuntu Linux 14.04 LTS**

Apache Tomcat in der Version 7 wird unter Ubuntu Linux 14.04 LTS aus den Standardrepositories mit dem folgenden Befehl installiert:

```bash
sudo aptitude install tomcat7
```

Der Dienst kann mit diesen beiden Befehlen gestoppt und gestartet werden:

```bash
service tomcat7 stop
service tomcat7 start
```

Die Konfigurationsdateien befinden sich unter:

```bash
/etc/tomcat7/
/etc/default/tomcat7/
```

Um Goobi zu installieren, muss die Datei goobi.war in den webapps-Ordner des Tomcat gelegt werden. Die Datei goobi.war wird automatisch entpackt. Der webapps-Ordner befindet sich unter folgendem Pfad:

```bash
/var/lib/tomcat7/webapps/
```