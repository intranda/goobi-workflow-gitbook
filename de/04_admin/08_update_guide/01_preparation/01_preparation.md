# Vorbereitung eines Updates

## Allgemeine Hinweise

Mit einem Update von Goobi workflow sollten auch alle Plugins aktualisiert werden. Dafür sollte am besten auch die Seite `Installierte Plugins` in Goobi workflow beachtet werden. Sollte diese hingegen noch nicht existieren, müssen die relevanten Dateien im Dateisystem identifiziert werden. Hierbei ist wichtig, auch die REST API nicht zu vergessen.

{% hint style="info" %}
Befehle aus dieser Anleitung werden am besten mit einem Klick auf das entsprechende Icon kopiert. Andernfalls besteht die Gefahr ungewollte Whitespaces mit zu kopieren.
{% endhint %}

## Sinnvolle Vorarbeiten vor Updatedurchführung

### Überprüfung des Zustands

Für einen guten Zustand des Systems sollten vor und/oder nach dem Update die folgenden Dinge geprüft werden:

* [ ] Konfigurationsdateien auf XML-Fehler prüfen:

```bash
find /opt/digiverso/goobi/{rulesets,config} /opt/digiverso/itm/{config,templates} /etc/tomcat9  -name "*.xml" -exec xmllint --noout {} \;
```

* [ ] Es kann vorkommen, dass in der Datenbank Benutzeraccounts ohne Authentifizierungsart stehen. Diese können mit dem folgenden SQL Statement zur Korrektur ermittelt werden. Sofern das Kommando etwas ausgibt, müssen die entsprechenden Benutzer in der Datenbanktabelle gesucht und korrigiert werden:

```bash
mysql goobi -e'SELECT DISTINCT ldapgruppenid FROM benutzer WHERE ldapgruppenid NOT IN (SELECT ldapgruppenid FROM ldapgruppen) OR ldapgruppenid IS NULL'
```

* [ ] Für alle Datenbanktabellen verwendet Goobi workflow `InnoDB`:

```bash
mysql goobi -NBse 'SELECT table_name FROM INFORMATION_SCHEMA.TABLES where TABLE_SCHEMA="goobi" and TABLE_TYPE="BASE TABLE" and ENGINE != "InnoDB"' | while read i; do echo $i; mysql goobi -e "alter table $i ENGINE = InnoDB"; done
```

* [ ] **goobi_opac.xml**: Bei mehrbändigen Werken muss der `rulesetChildType` gesetzt sein ([Vorlage](https://github.com/intranda/goobi-workflow/blob/master/Goobi/install/config/goobi_opac.xml#L36)).
* [ ] **goobi_projects.xml**: Es darf kein `BoundBook` mehr auftauchen ([Vorlage](https://github.com/intranda/goobi-workflow/blob/master/Goobi/install/config/goobi_projects.xml)).

### Erstellung eines Backups

Sinnvollerweise wird vor dem Backup der Tomcat ausgestellt. Allerdings ist vorher notwendig zu prüfen, dass kein Anwender mehr in Goobi workflow angemeldet ist. Neben der Anzeige der angemeldeten Benutzer in der Oberfläche können die letzten Einträge im Prozesslog oder die letzten Logins für die Bewertung der Lage hilfreich sein:

```bash
mysql goobi -e'select creationDate, userName, type, left(content,70) from journal order by creationDate desc limit 30'
grep user\ DN /opt/digiverso/logs/goobi.log -B1 | tail
# active users, needs /currentusers configured in goobi_rest.xml
PW=$(xmlstarlet sel -t -v '//endpoint[@path="/currentusers"]//allow[1]/@token' -n /opt/digiverso/goobi/config/goobi_rest.xml) && curl -X GET -H "token: $PW" localhost:8080/goobi/api/currentusers -s | jq
```

Anschließend kann der Tomcat Prozess für Goobi workflow beendet werden:

```bash
systemctl stop tomcat9
```

Mit den folgenden Befehlen können ein Backupverzeichnis erstellt und die Dateien dorthin kopiert werden:

```bash
BAK=/home/intranda/BACKUP/$(date -I) && mkdir $BAK -p
mysqldump goobi | gzip > $BAK/goobi.$(date +%s).sql.gz
mkdir $BAK/goobi $BAK/webapps
cp -at $BAK/goobi /opt/digiverso/goobi/{config,lib,plugins,rulesets,scripts,static_assets,xslt}
cp -at $BAK/webapps /var/lib/tomcat9/webapps/goobi
# If intranda TaskManager is installed
cp -at $BAK/webapps /var/lib/tomcat9/webapps/itm
cp -at $BAK/ /opt/digiverso/itm
# If LayoutWizzard is installed
cp -at $BAK /opt/digiverso/[L,l]ayout[w,W]izzard
```

Aktuellen Zustand im Goobi-Verzeichnis committen:

```bash
git -C /opt/digiverso/goobi/ add -A ; git -C /opt/digiverso/goobi/ commit -a -m 'pre update'
```

Aktuellen Zustand der Archive speichern:

Wenn ein Update von einer Version kleiner als 24.07 auf die aktuelle Version durchgeführt wird, müssen alle EAD-Dateien aus BaseX exportiert werden. Wenn es keine Archive gibt, kann dieser Punkt ignoriert werden.
Dafür unter `https://URL/basex/dba/login` einloggen. Dann unter `Databases` jede Datenbank auswählen, die .xml-Datei auswählen und herunterladen.

### Kopieren der neuen Dateien auf das System

Es empfiehlt sich, die Dateien auf dem zu aktualisierenden System nach `/tmp/g3` zu kopieren. Die Dateien in die korrekten Ordner verschieben:

```bash
U=/tmp/g3
G=/opt/digiverso/goobi

mv ${U:-/tmp/g3}/goobi.war /var/lib/tomcat9/webapps/

# find ${G:-/opt/digiverso/goobi}/{lib,plugins} -name 'plugin*jar' -delete

mv ${U:-/tmp/g3}/statistics_template.* ${G:-/opt/digiverso/goobi}/plugins/statistics/
mv ${U:-/tmp/g3}/plugin*-gui.jar ${G:-/opt/digiverso/goobi}/plugins/GUI/
mv ${U:-/tmp/g3}/plugin*-lib.jar ${G:-/opt/digiverso/goobi}/lib/
mv ${U:-/tmp/g3}/plugin*-api.jar ${G:-/opt/digiverso/goobi}/lib/
mv ${U:-/tmp/g3}/plugin*-job.jar ${G:-/opt/digiverso/goobi}/lib/

find ${U:-/tmp/g3} -name 'plugin-*-base.jar' -printf '%f\n' | awk -F'-' '{print $0"\t"$2}' | while read -r file type; do
    mv "/tmp/g3/${file}" "${G:-/opt/digiverso/goobi}/plugins/${type}/"
done

# If intranda TaskManager is installed
mv ${U:-/tmp/g3}/itm.war /var/lib/tomcat9/webapps/
mv ${U:-/tmp/g3}/TaskClient.jar /opt/digiverso/itm/bin/TaskClient.jar

# If LayoutWizzard is installed
cp -p ${U:-/tmp/g3}/LayoutWizzard-jar-with-dependencies.jar ${G:-/opt/digiverso/goobi}/lib/
cp -p ${U:-/tmp/g3}/LayoutWizzard-jar-with-dependencies.jar /opt/digiverso/itm/lib/
```

{% hint style="info" %}
Gerade Konfigurationsdateien von Plugins können aufgrund einer Änderung des Schemas für die Benennung inzwischen einen anderen Dateinamen haben.
{% endhint %}

Nach Abschluss der Arbeiten kann über den Abgleich der Zeitstempel ermittelt werden, ob alle notwendigen Dateien aktualisiert wurden:

```bash
ls -lh /opt/digiverso/goobi/plugins/*/*
ls -lh /opt/digiverso/goobi/lib/*
```

Plugins, die als `Tar`-Paket gebaut werden:

```bash
goobiInstallPlugin() {
    tar -C /opt/digiverso/goobi/ -xvf $1 --exclude "pom.xml"
}
# Example:
goobiInstallPlugin /tmp/g3/plugin_intranda_step_replace-images.tar
```

### Testen des installierten Updates

Die folgenden Dinge sollten nach einem Update geprüft werden:

* [ ] Annehmen und Abgeben von Aufgaben, insbesondere das Verlinken (gegebenenfalls Mounten) des Image-Ordners ins Homeverzeichnis
* [ ] Bildanzeige im ImageQA Plugin
* [ ] Bild- und Thumbnailanzeige im Metadateneditor
* [ ] Bildanzeige im LayoutWizzard Plugin
* [ ] Generierung von Laufzetteln
* [ ] Übergabe von Jobs an den intranda TaskManager sowie eine Rückmeldung im Vorgangslog wenn ein Job im TaskManager abgebrochen wird (bei Änderungen an der Kommunikation zwischen Goobi workflow und dem TaskManager)
* [ ] Katalogabfragen
* [ ] Alle Plugins sind aktuell in: Administration -> Installierte Plugins

### Rescue im Falle von auftretenden Problemen

Manchmal kann es vorkommen, dass nach dem Update Fehler auftreten. Die folgenden Punkte helfen dabei, typische Probleme zu identifizieren und zu beheben:

#### **Goobi startet nicht - ActiveMQ**

Wenn der Tomcat nach dem Start hängen bleibt, kann der Inhalt des Ordners `/opt/digiverso/goobi/activemq/` daran Schuld sein. Leeren und neu starten hilft in diesem Fall:

```bash
find /opt/digiverso/goobi/activemq/ -type f -delete
```

#### **LayoutWizzard**

Die `LayoutWizzard.jar` in `/opt/digiverso/{goobi,itm}/lib/` müssen gleich sein. Symbolische Links funktionieren nicht.

## Durchführung des eigentlichen Updates

Nachdem alle Vorarbeiten durchgeführt wurden, kann das eigentliche Update erfolgen. Dieses ist in einzelnen Schritten detailliert hier erläutert:

{% page-ref page="../02_update_steps/02_update_steps.md" %}