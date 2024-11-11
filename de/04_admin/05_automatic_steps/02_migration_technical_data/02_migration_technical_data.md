# Migration technischer Metadaten in METS-Dateien

Goobi exportiert automatisch die METS-Dateien in einen definierten Ordner. Dies ist zumeist das folgende Verzeichnis:

```bash
/opt/digiverso/viewer/hotfolder/
```

In diesem Verzeichnis wird für jeden Vorgang ein Unterordner erzeugt. Innerhalb dieses erzeugten Ordners werden nun alle zu exportierenden Daten kopiert. Das beinhaltet neben der eigentlichen METS-Datei unter Umständen ebenso die Anchor-Datei, die Bilder sowie OCR Daten.

Nachdem der Export erfolgreich durchgeführt wurde, wird ein Programm namens `PostExport.jar` aufgerufen. Dieses Programm greift auf die exportierte METS Datei zu, benennt diese um, so dass der Dateiname der b-Nummer entspricht und merged diese mit der SDB-AMD Datei.

Im ersten Schritt wird dabei die AMD-Datei eingelesen und für jedes File-Element ein Element `mets:techMD` innerhalb der Sektion `mets:amdSec` der METS Datei angelegt. Im zweiten Schritt werden die FileGroups durchlaufen und Dateiname, Checksum und Mimetype aus den Werten der AMD Datei gebildet. Als letztes werden die Strukturelemente der physischen structMap mit den einzelnen techMD verbunden.  
Anschließend wird die so angereicherte METS Datei an den definierten Ordner geschrieben, von dem aus die Präsentation die Daten einlesen kann.

Für den Fall, dass es sich bei den Daten um `multiple manifestation objects` handelt, bei denen bereits eine oder mehrere manifestations exportiert wurden, werden nun noch die anchor-Dateien gemerged. Hierbei wird ein neues Child-Element in die logische structMap eingetragen, das die Informationen des neuen Objekts enthält. Die Reihenfolge innerhalb der structMap wird durch das Metadatum `order number` definiert.