# Unterverzeichnis ‚metadata’

Das Verzeichnis `metadata` ist das zentrale Verzeichnis für die Speicherung von Metadaten und digitalen Inhalten von Goobi. Innerhalb dieses Verzeichnisses befindet sich für jeden Goobi-Vorgang ein Verzeichnis mit dem Namen der Vorgangs-ID von Goobi. Die Verzeichnisse der einzelnen Goobi-Vorgänge sind dabei folgendermaßen aufgebaut:

```bash
└── 1234
    ├── export
    │   └── ...
    ├── images
    │   └── ...
    ├── import
    │   └── ...
    ├── ocr
    │   └── ...
    ├── taskmanager
    │   └── ...
    ├── thumbs
    │   └── ...
    ├── validation
    │   └── ...
    └── meta.xml
```

Neben der zentralen Metadatendatei `meta.xml` befinden sich je nach Konfiguration gegebenenfalls noch weitere Backupdateien wie z.B. `meta.xml-2021-11-28-175618166`, `meta.xml.2024-05-08-135432256`, etc. in dem Verzeichnis.


## Verzeichnis `images`
Das Verzeichnis `images` wird innerhalb des Workflows verschiedenen Nutzern temporär zur Verfügung gestellt und hat dabei den folgenden Aufbau:

```bash
└── 1234
    ├── images
    │   └── abc_8765432_raw
    │   │   └── 00000001.raw
    │   │   └── 00000002.raw
    │   │   └── 00000003.raw
    │   │   └── 00000004.raw
    │   │   └── 00000005.raw
    │   ├── abc_8765432_master
    │   │   └── 00000001.tif
    │   │   └── 00000002.tif
    │   │   └── 00000003.tif
    │   │   └── 00000004.tif
    │   │   └── 00000005.tif
    │   └── abc_8765432_media
    │   │   └── 00000001.jpg
    │   │   └── 00000002.jpg
    │   │   └── 00000003.jpg
    │   │   └── 00000004.jpg
    │   │   └── 00000005.jpg
    │   └── abc_8765432_source
    │       └── source_files_1.pdf
    │       └── source_files_2.xls
    │       └── source_files_3.wmv
    └── meta.xml
```

### Unterverzeichnis `media`
Der für die Arbeit mit den Inhalten wichtigste Ordner ist derjenige, der auf `_media` endet. Hier werden diejenigen Dateien abgelegt, die für eine Veröffentlichung (z.B. in einem Goobi viewer) verwendet werden sollen. Die hier gespeicherten Dateien sind üblicherweise komprimierte Derivate, die für die Arbeit mit dem Digitalisat und deren Veröffentlichung in sehr guter Qualität verwendet werden können.

### Unterverzeichnis `master`
Innerhalb des Verzeichnisses, dass auf `_master` endet, finden sich die Master-Dateien. Hierbei handelt es sich üblicherweise um die unveränderten Originale, wie sie z.B. von Scannern erzeugt werden. Sie sind typischerweise unkomprimiert und auch nicht anderweitig optimiert (gerade gerückt, gecroppt oder ähnliches).

### Unterverzeichnis `source`
In dem Verzeichnis, dessn Name auf `_source` endet, können Quelldateien abgelegt werden, auf die die Goobi-Anwender ggf. ebenfalls Zugriff haben sollen, um diese hochzuladen oder einzusehen. Die hier abgelegten Dateien werden im Rahmen des Standardexports von Goobi workflow berücksichtigt und mit exportiert. Im Falle es Exports zum Goobi viewer bedeutet dies beispielsweise, dass die Daten aus dem Source-Ordner ebenfalls in den `hotfolder` des Goobi viewers exportiert werden.

### Weitere Unterverzeichnisse
Neben den hier genannten Verzeichnissen können auch weitere Unterverzeichnisse vorhanden sein. Als Beispiel ist hier ein Verzeichnis aufgeführt, dessen Name auf `_raw` endet, um dort beispielsweise RAW-Dateien von Kameras oder auch andere Daten abzulegen. Auch auf diese Ordner können die Nutzer von Goobi somit Zugriff erhalten. Eine Erläuterung, wie solche zusätzlichen Verzeichnisse in Goobi workflow konfiguriert werden, [findet sich hier](../../../06_config_files/02_goobi_config.properties/02_goobi_config.properties.md).


## OCR
Neben dem Verzeichnis `images` kann ebenfalls ein Verzeichnis `ocr` vorhanden sein. Hierin befinden sich sämtliche OCR-Ergebnisse, die innerhalb des Workflows erzeugt und zu dem Vorgang hinzugefügt wurden. Für jedes vorliegende Format der OCR-Ergebnisse besteht ein eigenes Verzeichnis mit den jeweiligen Dateien darin.

```bash
└── 1234
    └── ocr
        └── abc_8765432_alto
        │   └── 00000001.xml
        │   └── 00000002.xml
        │   └── 00000003.xml
        │   └── 00000004.xml
        │   └── 00000005.xml
        ├── abc_8765432_doc
        │   └── 00000001.doc
        │   └── 00000002.doc
        │   └── 00000003.doc
        │   └── 00000004.doc
        │   └── 00000005.doc
        └── abc_8765432_pdf
            └── 00000001.pdf
            └── 00000002.pdf
            └── 00000003.pdf
            └── 00000004.pdf
            └── 00000005.pdf
```


## Thumbnails
Im Ordner `thumbs` können kleinere Versionen der in `images` liegenden Bilder gespeichert werden, die Goobi verwendet um die Bilder in geringer Auflösung darzustellen. Dies erhöht die Geschwindigkeit der Bildanzeige bei größeren Bildern erheblich. Für jeden Unterordner von `images` können ein oder mehrere Unterordner in `thumbs` angelegt werden, die den selben Namen tragen wie der `images`-Unterordner, erweitert um einen zusätzlichen Unterstrich _ und eine Größenangabe in Pixeln. Diese Größenangabe muss dem Maximum von Höhe und Breite der Bilder im jeweiligen Unterordner entsprechen. Die Dateinamen der Bilder im `thumbs` Unterordner müssen denen der Bilder im passenden `images` Unterordner entsprechen, jedoch mit der Dateiendung `.jpg`.

```bash
└── 1234
    └── thumbs
        └── abc_8765432_master_800
        │   └── 00000001.jpg
        │   └── 00000002.jpg
        │   └── 00000003.jpg
        │   └── 00000004.jpg
        │   └── 00000005.jpg
        ├── abc_8765432_master_3000
        │   └── 00000001.jpg
        │   └── 00000002.jpg
        │   └── 00000003.jpg
        │   └── 00000004.jpg
        │   └── 00000005.jpg
        ├── abc_8765432_media_800
        │   └── 00000001.jpg
        │   └── 00000002.jpg
        │   └── 00000003.jpg
        │   └── 00000004.jpg
        │   └── 00000005.jpg
        └── abc_8765432_media_3000
            └── 00000001.jpg
            └── 00000002.jpg
            └── 00000003.jpg
            └── 00000004.jpg
            └── 00000005.jpg
```

Wenn zu einer Bilddatei in `images` passende Bilder in `thumbs` vorhanden sind, dann werden diese in Goobi automatisch verwendet für die Anzeige von Thumbnails und zoombaren Bildern im herausgezoomten Zustand.


## Validierung
Sollte auf dem Goobi-Server und auch in den verwendeten Workflows eine automatische Validierung z.B. der Images stattfinden, existiert das Verzeichnis `validation`.

Innerhalb dieses Verzeichnisses wird pro Validierungsdurchführung jeweils ein Unterordner erzeugt, um auch ältere Validierungsergebnisse vorzuhalten. Die Benennung der erzeugten Unterordner erfolgt dabei stets so, dass der Ordnername sowohl Datum und Uhrzeit sowie den Typ der Validierung aufführen. Dies sieht z.B. wie folgt aus:

```bash
└── 1234
    └── validation
        └── 2022-11-20_11-20-01_jpylyzer
        │   └── 00000001.xml
        │   └── 00000002.xml
        │   └── 00000003.xml
        │   └── 00000004.xml
        │   └── 00000005.xml
        ├── 2022-11-20_12-02-13_jhove
        │   └── 00000001.xml
        │   └── 00000002.xml
        │   └── 00000003.xml
        │   └── 00000004.xml
        │   └── 00000005.xml
        └── 2022-11-23_08-12-56_jpylyzer
            └── 00000001.xml
            └── 00000002.xml
            └── 00000003.xml
            └── 00000004.xml
            └── 00000005.xml
```

Findet eine Zusammenarbeit mit dem intranda TaskManager statt, so existiert innerhalb des Ordners ebenso das Verzeichnis `taskmanager`. Binnen dieses Verzeichnisses speichert der TaskManager temporäre Daten für die Durchführung langlaufender Aufgaben. Außerdem werden an dieser Stelle je nach Konfiguration ebenfalls sämtliche Ticket- bzw. Templatedateien dauerhaft gespeichert und vorgehalten, die für die einzelnen Aufrufe des TaskManagers verwendet wurden. Der Inhalt dieses Verzeichnisses sieht folgendermaßen aus:

```bash
└── 1234
    └── taskmanager
        └── 2022-11-23_08-12-56_jp2validate
        │   └── 00000001.xml
        │   └── 00000002.xml
        │   └── 00000003.xml
        │   └── 00000004.xml
        │   └── 00000005.xml
        └── 2022-11-25_14-38-15_iii-create_jpeg
            └── 00000001.jpeg
            └── 00000002.jpeg
            └── 00000003.jpeg
            └── 00000004.jpeg
            └── 00000005.jpeg
```


## Import
Auch abhängig von der individuellen Installation liegt pro Goobi-Vorgang gleichermaßen ein Ordner `import` vor. Dieser Ordner wird von Import-Plugins dafür verwendet originale Quelldateien zum jeweiligen Vorgang zugehörig mitzuführen. Eingespielte und importierte Katalogdatensatzdateien oder andere Ursprungsdateien können hier aufbewahrt und innerhalb von Scripten im Rahmen der Workflowverarbeitung verwendet werden. Der Inhalt des Ordners könnte z.B. folgendermaßen aussehen:

```bash
└── 1234
    └── import
        └── eod
        │   └── 00000001.tif
        │   └── 00000002.tif
        │   └── 00000003.tif
        │   └── 00000004.tif
        │   └── 00000005.tif
        ├── abc.mrc
        └── abc.original.pdf
```

## Export
Auch ein Ordner mit dem Namen `export` kann innerhalb des Vorgangsverzeichnisses vorhanden sein. In diesem können Dateien in gleicher Struktur wie innerhalb des `images`-Verzeichnisses gespeichert werden. Die hier vorhandenen Dateien werden dann im Rahmen des Exports mit berücksichtigt und z.B. in den Hotfolder des Goobi viewers exportiert. Dies könnte dann erforderlich sein, wenn Dateien für den Export berücksichtig werden sollen, ohne dass sie im images-Ordner vorhanden sein sollen und ohne dass sie innerhalb der METS-Datei referenziert werden. 

Der Inhalt könnte beispielsweise so aussehen:


```bash
└── 1234
    └── export
        └── abc_8765432_media
            └── intro.mp3
            └── overview.jpg
            └── some_file.pdf
```