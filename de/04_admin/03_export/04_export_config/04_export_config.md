# Konfiguration des Exports in der Goobi Konfigurationsdatei

Der Export kann innerhalb der Konfigurationsdatei `goobi_config.properties` weitergehend konfiguriert werden. Der hierbei wichtige Parameter lautet:

```ini
exportWithoutTimeLimit=true|false
```

Wenn dieser Wert auf `true` gesetzt ist, gibt Goobi eine Erfolgsmeldung über den erfolgreichen Export aus, sobald das Kopieren der exportierten Dateien in die in den Projekteinstellungen definierten Ordner `DMS-Export-Ordner für XML-`Datei und `DMS-Export-Images-Ordner` erfolgreich abgeschlossen wurde. Goobi gibt eine Fehlermeldung aus, falls während des Kopiervorgangs ein Fehler aufgetreten ist.

Ist dieser Wert hingegen auf `false` gesetzt, oder fehlt in der Konfigurationsdatei, gibt Goobi eine Erfolgsmeldung über den erfolgreichen Export erst dann aus, falls eine entsprechende Meldung in dem innerhalb des in den Projekteinstellungen definierten Ordners `DMS-Export-Success-Ordner` gefunden werden kann. Goobi gibt eine Fehlermeldung aus, wenn es eine Fehlermeldung innerhalb des Verzeichnisses `DMS-Export-Error-Ordner` vorfindet. 

Wenn Goobi innerhalb des in den Projekteinstellungen definierten Zeitintervalls für die Zeitüberschreitung keine Meldung im `Success` oder `Error` Ordner findet, löscht es die exportierten Werke automatisch.