# Einbindung von S3 als Storage

Goobi workflow erlaubt den Betrieb mit S3-kompatiblem Storage. Dabei ist zu beachten, dass weiterhin ein lokales Dateisystem benötigt wird, um die Metadaten abspeichern zu können. Dies bedeutet, dass die Dateien `meta.xml`, `meta_anchor.xml` sowie ihre Backups, die für den jeweiligen Vorgang vorhanden sind, auch weiterhin im Dateisystem gespeichert werden. Lediglich alle anderen Daten, wie beispielsweise Bilder und OCR-Ergebnisse, werden auf dem S3-Speicherbereich gelagert.

Um Goobi mit S3 als Storage betreiben zu können, müssen die beiden folgenden Einstellungen innerhalb der Konfigurationsdatei `goobi_config.properties` gesetzt werden:

```ini
# global config if s3 should be used
useS3=true

# the bucket that is used for the content that would normally live in /opt/digiverso/goobi/metadata/
S3bucket=workflow-data
```

Goobi workflow nutzt intern das AWS Java SDK. Das heißt, die Zugangsdaten für den Zugriff auf das Speichersystem werden entweder aus `$HOME/.aws` oder aus Umgebungsvariablen gelesen. Wenn statt AWS ein anderer S3-Provider zum Einsatz kommen soll, kann die Anbindung relativ granular konfiguriert werden. Dazu werden noch einige weitere Einstellungen innerhalb der gleichen Konfigurationsdateien benötigt:

```ini
S3AccessKeyID=keyID
S3SecretAccessKey=secretkey
S3Endpoint=http://s3.mygoobi.tld
```

Ein Einsatz von S3 als Speichersystem sollte grundsätzlich mit allen S3-kompatiblen APIs funktionieren. Während der Entwicklung der S3-Funktionalität kam für die Implementierung sowohl Amazon S3 als auch [MinIO](https://min.io/) zum Einsatz.