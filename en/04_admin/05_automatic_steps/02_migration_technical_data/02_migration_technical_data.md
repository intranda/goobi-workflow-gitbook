# Migration of technical data to METS files

Goobi automatically exports METS files to a pre-defined folder. This is usually the directory shown below:

```bash
/opt/digiverso/viewer/hotfolder/
```

A sub-folder is created in this directory for each process, and all the data being exported is copied within this new folder. As well as the actual METS file, this may include the anchor file, the images and OCR data.

Once the export has been completed, Goobi calls `PostExport.jar`. This program renames the exported METS file (so that the file name corresponds with the b-number) and merges it with the SDB-AMD file.

As a first step, this involves reading in the AMD file and for each element creating a `mets:techMD` element within the `mets:amdSec` section of the METS file. The second step involves checking all the FileGroups individually. The file name, checksum and Mime type are formed from the values in the AMD file. Finally, the structure elements of the physical structMap are linked to the individual techMD.

After this, the enriched METS file is written to the pre-defined folder, and from here the presentation can read in the data.

If the data includes `multiple manifestation objects` and one or more manifestations have already been exported, the anchor files are also merged. This involves entering into the logical structMap a new child element that contains the information for the new object. The sequence within the structMap is defined using the metadata item `order number`.