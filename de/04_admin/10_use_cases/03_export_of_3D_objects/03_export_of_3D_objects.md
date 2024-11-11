---
description: >-
  Um Vorgänge mit 3D-Objekten in den Goobi-Viewer oder andere Präsentationssysteme korrekt zu exporieren sind einige zusätzliche Vorkehrungen notwendig.
---

# Export von 3D-Objekten in den Goobi viewer

## Installation des 3D-Export Plugins für Goobi

Für den Export von 3D-Objekten mit Hilfsdateien (mtl, Oberflächenbilder, ...) muss der Export mit folgendem Goobi-Export-Plugin durchgeführt werden:

```bash
plugin_intranda_export_object3d.jar
```

Das Plugin muss im Export-Schritt als `Plugin für Arbeitsschritt` eingetragen sein.

## Konfiguration der METS-Dateigruppen

Damit auch 3D-Objekte beim Export mit dem 3D-Export Plugin in die METS-Datei geschrieben werden, muss in der Projektkonfiguration eine zusätzliche METS-Dateigruppe angelegt werden mit folgenden Eigenschaften:

| Bezeichnung | Wert |
| :--- | :--- |
| Name: | `OBJECT` |
| Pfad: | `file:///opt/digiverso/viewer/media/$(meta.CatalogIDDigital)/` |
| MIME Typ: | `application/object` |
| Suffix: | `obj / glb / ...` |

Der Wert in `Suffix` muss dabei immer genau der Dateiendung der zu exportierenden 3D-Objekte entsprechen.