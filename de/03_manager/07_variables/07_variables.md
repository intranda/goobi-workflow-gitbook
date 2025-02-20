# Variablensystem

Goobi kann an verschiedenen Stellen auf Variablen zugreifen. Dabei gibt es einige Variablen, die nur in bestimmten Kontexten verwendet werden dürfen. Hierzu zählen zum Beispiel die Variablen `{login}` oder `{user full name}` bei der LDAP Konfiguration.

Desweiteren gibt es die sogenannten statischen und dynamischen Variablen. Diese Variablen können an verschiedenen Stellen genutzt werden. Sie stehen zum Beispiel bei Skriptaufrufen oder der Projektkonfiguration zur Verfügung.

## Statische Variablen

Statische Variablen sind Variablen, die einen festen Namen und einen definierten Wert haben.

### Statische Variable: {prefs}

| Variable: | {prefs} |
| :--- | :--- |
| Beispielwert: | /opt/digiverso/goobi/rulesets/ruleset.xml |
| Bedeutung: | Dies ist der absolute Pfad zur Regelsatzdatei, die im Vorgang angegeben ist. |

### Statische Variable: {processid}

| Variable: | {processid} |
| :--- | :--- |
| Beispielwert: | 27 |
| Bedeutung: | Dies ist der interne Identifier, mit dem der Vorgang in Goobi verknüpft ist. |

### Statische Variable: {processtitle}

| Variable: | {processtitle} |
| :--- | :--- |
| Beispielwert: | kleiuniv_PPN517154005 |
| Bedeutung: | Dies ist der Titel des Vorgangs. |

### Statische Variable: {stepid}

| Variable: | {stepid} |
| :--- | :--- |
| Beispielwert: | 6519 |
| Bedeutung: | Dies ist der interne Identifier, mit dem der Schritt in Goobi verknüpft ist. Diese Variable kann nur bei Skriptaufrufen genutzt werden. |

### Statische Variable: {stepname}

| Variable: | {stepname} |
| :--- | :--- |
| Beispielwert: | scanning |
| Bedeutung: | Dies ist der Titel des Arbeitsschrittes. Diese Variable kann nur bei Skriptaufrufen genutzt werden. |

### Statische Variable: {processpath}

| Variable: | {processpath} |
| :--- | :--- |
| Beispielwert: | /opt/digiverso/goobi/metadata/27/ |
| Bedeutung: | Der absolute Pfad zum Ordner, in dem sich alle Daten des Vorgangs befinden. |

### Statische Variable: {importpath}

| Variable: | {importpath} |
| :--- | :--- |
| Beispielwert: | /opt/digiverso/goobi/metadata/27/import |
| Bedeutung: | Der absolute Pfad zum import-Ordner des Vorgangs. Es handelt sich dabei um einen Unterordner von {processpath}. In diesem Ordner befinden sich Dateien, die während des Imports erzeugt oder importiert wurden. |

### Statische Variable: {imagepath}

| Variable | {imagepath} |
| :--- | :--- |
| Beispielwert: | /opt/digiverso/goobi/metadata/27/images |
| Bedeutung: | Der absolute Pfad zum images-Ordner des Vorgangs. Es handelt sich dabei um einen Unterordner von {processpath}. In diesem Ordner befinden sich verschiedene Ordner für die einzelnen Digitalisate. |

### Statische Variable: {tifpath}

| Variable: | {tifpath} |
| :--- | :--- |
| Beispielwert: | /opt/digiverso/goobi/metadata/27/images/kleiuniv_PPN517154005_media |
| Bedeutung: | Der absolute Pfad zum media-Ordner des Vorgangs. Es handelt sich dabei um einen Unterordner von {imagepath}. In diesem Ordner befinden sich die optimierten Digitalisate. Dieser Ordner wird üblicherweise am Ende des Workflows exportiert. |

### Statische Variable: {origpath}

| Variable: | {origpath} |
| :--- | :--- |
| Beispielwert: | /opt/digiverso/goobi/metadata/27/images/master_kleiuniv_PPN517154005_media |
| Bedeutung: | Der absolute Pfad zum master-Ordner des Vorgangs. Es handelt sich dabei um einen Unterordner von {imagepath}. In diesem Ordner befinden sich die erstellten Scans.  Aus diesem Ordner werden üblicherweise die Derivate für die anderen Ordner erzeugt. |

### Statische Variable: {metaFile}

| Variable: | {metaFile} |
| :--- | :--- |
| Beispielwert: | /opt/digiverso/goobi/metadata/27/meta.xml |
| Bedeutung: | Der absolute Pfad zur Metadatendatei in Goobi. Diese Datei kann in verschiedenen Formaten vorliegen. |

### Statische Variable: {tifurl}

| Variable: | {tifurl} |
| :--- | :--- |
| Beispielwert: | [file:///opt/digiverso/goobi/metadata/27/images/kleiuniv_PPN517154005_media](file:///opt/digiverso/goobi/metadata/27/images/kleiuniv_PPN517154005_media) |
| Bedeutung: | Der Pfad von {tifpath} als gültige URL. |

### Statische Variable: {origurl}

| Variable: | {origurl} |
| :--- | :--- |
| Beispielwert: | [file:///opt/digiverso/goobi/metadata/27/images/master_kleiuniv_PPN517154005_media](file:///opt/digiverso/goobi/metadata/27/images/master_kleiuniv_PPN517154005_media) |
| Bedeutung: | Der Pfad von {origpath} als gültige URL. |

### Statische Variable: {sourcepath}

| Variable: | {sourcepath} |
| :--- | :--- |
| Beispielwert: | /opt/digiverso/goobi/metadata/27/images/kleiuniv_PPN517154005_source/ |
| Bedeutung: | Der Pfad zum source-Ordner des Vorgangs. Hier können Dateien hinterlegt werden, die zusätzlich beim Export in den Goobi viewer mit übergeben werden sollen. |

### Statische Variable: {projectid}

| Variable: | {projectid} |
| :--- | :--- |
| Beispielwert: | 4 |
| Bedeutung: | Die interne ID des Projektes innerhalb der Goobi workflow Datenbank. |

### Statische Variable: {projectname}

| Variable: | {projectname} |
| :--- | :--- |
| Beispielwert: | Monographien 1850-1950 |
| Bedeutung: | Der Name des Projektes innerhalb der Goobi workflow Datenbank. |

### Statische Variable: {projectidentifier}

| Variable: | {projectidentifier} |
| :--- | :--- |
| Beispielwert: | M1850-1950 |
| Bedeutung: | Der sprechende Identifier, der dem Projekt unabhängig von der Datenbank-ID zusätzlich gegeben wurde. |

### Statische Variable: {iiifMediaFolder}

| Variable: | {iiifMediaFolder} |
| :--- | :--- |
| Beispielwert: | "[http://example.com/goobi/api/process/image/12345/schudiss_618299084_media/00000001.tif/full/max/0/default.jpg?jwt=1234567890](http://example.com/goobi/api/process/image/12345/schudiss_618299084_media/00000001.tif/full/max/0/default.jpg?jwt=1234567890)", "[http://example.com/goobi/api/process/image/12345/schudiss_618299084_media/00000002.tif/full/max/0/default.jpg?jwt=0987654321](http://example.com/goobi/api/process/image/12345/schudiss_618299084_media/00000002.tif/full/max/0/default.jpg?jwt=0987654321)", ... |
| Bedeutung: | Auflistung von IIIF-URLs zu allen Bildern aus dem `media`-Verzeichnis eines Vorgangs |

### Statische Variable: {iiifMasterFolder}

| Variable: | {iiifMasterFolder} |
| :--- | :--- |
| Beispielwert: | "[http://example.com/goobi/api/process/image/12345/schudiss_618299084_master/00000001.tif/full/max/0/default.jpg?jwt=1234567890](http://example.com/goobi/api/process/image/12345/schudiss_618299084_master/00000001.tif/full/max/0/default.jpg?jwt=1234567890)", "[http://example.com/goobi/api/process/image/12345/schudiss_618299084_master/00000002.tif/full/max/0/default.jpg?jwt=0987654321](http://example.com/goobi/api/process/image/12345/schudiss_618299084_master/00000002.tif/full/max/0/default.jpg?jwt=0987654321)", ... |
| Bedeutung: | Auflistung von IIIF-URLs zu allen Bildern aus dem `master`-Verzeichnis eines Vorgangs |

## Dynamische Variablen

Neben den statischen Variablen existieren noch eine Reihe dynamischer Variablen, mit denen der Zugriff auf alle frei konfigurierbaren Daten in Goobi möglich ist.

### Dynamische Variable: {process.NAME}

| Variable: | {process.NAME} |
| :--- | :--- |
| Beispiel: | {process.b-number} |
| Beispielwert: | b20057465 |
| Bedeutung: | Mit dieser Variable kann auf den Wert jeder Vorgangseigenschaft zugegriffen werden. |

### Dynamische Variable: {product.NAME}

| Variable: | {product.NAME} |
| :--- | :--- |
| Beispiel: | {product.Artist} |
| Beispielwert: | Niedersächsische Staats- und Universitätsbibliothek Göttingen, Germany |
| Bedeutung: | Mit dieser Variable kann auf den Wert jeder Werkstücksseigenschaft zugegriffen werden. |

### Dynamische Variable: {template.NAME}

| Variable: | {template.NAME} |
| :--- | :--- |
| Beispiel: | {template.Shelfmark} |
| Beispielwert: | 8 HLP II, 8726 |
| Bedeutung: | Mit dieser Variable kann auf den Wert jeder Vorlageeigenschaft zugegriffen werden. |

### Dynamische Variable: {meta.NAME}

| Variable: | {meta.NAME} |
| :--- | :--- |
| Beispiel: | {meta.PlaceOfPublication} |
| Beispielwert: | Göttingen |
| Bedeutung: | Mit dieser Variable kann der Wert eines Metadatums genutzt werden. Dabei wird die Metadatendatei rekursiv durchsucht und der erste gefundene Wert genutzt. |

### Dynamische Variable: {meta.topstruct.NAME}

| Variable: | {meta.topstruct.NAME} |
| :--- | :--- |
| Beispiel: | {meta.topstruct.CatalogId Digital} |
| Beispielwert: | 517154005 |
| Bedeutung: | Mit dieser Variable kann der Wert eines Metadatums genutzt werden. Dabei wird nur das oberste Strukturelement nach dem Metadatum durchsucht. |

### Dynamische Variable: {meta.firstchild.NAME}

| Variable: | {meta.firstchild.NAME} |
| :--- | :--- |
| Beispiel: | {meta.firstchild.CurrentNo} |
| Beispielwert: | 12 |
| Bedeutung: | Mit dieser Variable kann der Wert eines Metadatums genutzt werden, das sich im ersten Unterelement des Hauptelementes befindet. Dies wird insbesondere bei mehrbändigen oder periodischen Strukturen benötigt. |

### Dynamische Variable: {db_meta.NAME}

| Variable: | {db_meta.NAME} |
| :--- | :--- |
| Beispiel: | {db_meta.DocStruct} |
| Beispielwert: | Monograph |
| Bedeutung: | Mit dieser Variable kann der Wert eines Metadatums genutzt werden. Dieser wird in diesem Fall nicht aus der METS-Datei selbst gelesen, sondern stammt stattdessen aus der gecachten Version aus der Datenbank. |

### Dynamische Variable: {datetime.PATTERN}

| Variable: | {datetime.PATTERN} |
| :--- | :--- |
| Beispiel: | {datetime.dd.MM.yyyy} |
| Beispielwert: | 13.08.2024 |
| Bedeutung: | Mit dieser Variable kann der aktuelle Zeitpunkt (Datum und Uhrzeit) in beliebigen Formaten erzeugt werden. Das Format `PATTERN` kann dabei alle erlaubten Symbole zur Datums- und Zeitformatierung in Java enthalten. Mehr Informationen hierzu finden Sie unter: https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html |