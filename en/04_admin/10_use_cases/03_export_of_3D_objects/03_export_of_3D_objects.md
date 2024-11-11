---
description: >-
  In order to correctly export processes with 3D objects to the Goobi viewer or other presentation systems, some additional precautions are necessary.
---

# Export of 3D-Objects into the Goobi viewer

## Installing the 3D export plugin for Goobi

For the export of 3D objects with auxiliary files (mtl, surface images, ...) the export must be done with the following Goobi export plugin:

```bash
plugin_intranda_export_object3d.jar
```

The plugin must be entered in the export step as `Step Plugin`.

## Configuration of the METS file groups

To ensure that 3D objects are also written to the METS file when exporting with the 3D export plugin, an additional METS file group must be created in the project configuration with the following properties:

| Name | Value |
| :--- | :--- |
| Name: | `OBJECT` |
| Path: | `file:///opt/digiverso/viewer/media/$(meta.CatalogIDDigital)/` |
| MIME Typ: | `application/object` |
| Suffix: | `obj / glb / ...` |

The value in `Suffix` must always correspond exactly to the file extension of the 3D objects to be exported.