# Variables

Goobi can also use variables when performing certain actions. Some of these variables can be used only in specific contexts, e.g. the variables `{login}` and `{user full name}` when configuring the LDAP.

There are also ‘static’ and ‘dynamic’ variables. These can be used at various points, e.g. when calling scripts or configuring projects.

## Static variables

Static variables are variables with a fixed name and a defined value.

### Static variable: {prefs}

| Variable: | {prefs} |
| :--- | :--- |
| Sample value: | /opt/digiverso/goobi/rulesets/ruleset.xml |
| Meaning: | This is the absolute path to the ruleset file specified in the process. |

### Static variable: {processid}

| Variable: | {processid} |
| :--- | :--- |
| Sample value: | 27 |
| Meaning: | This is the internal identifier to which the process is linked in Goobi. |

### Static variable: {processtitle}

| Variable: | {processtitle} |
| :--- | :--- |
| Sample value: | kleiuniv_PPN517154005 |
| Meaning: | This is the process title. |

### Static variable: {stepid}

| Variable: | {stepid} |
| :--- | :--- |
| Sample value: | 6519 |
| Meaning: | This is the internal identifier to which the workflow step is linked in Goobi. This variable can be used only when calling scripts. |

### Static variable: {stepname}

| Variable: | {stepname} |
| :--- | :--- |
| Sample value: | scanning |
| Meaning: | This is the title of the workflow step. This variable can be used only when calling scripts. |

### Static variable: {processpath}

| Variable: | {processpath} |
| :--- | :--- |
| Sample value: | /opt/digiverso/goobi/metadata/27/ |
| Meaning: | The absolute path to the folder in which all the process data are located. |

### Static variable: {importpath}

| Variable: | {importpath} |
| :--- | :--- |
| Sample value: | /opt/digiverso/goobi/metadata/27/import |
| Meaning: | The absolute path to the import folder for the process. This is a subfolder of {processpath}. It contains the files that were generated or imported when performing an import. |

### Static variable: {imagepath}

| Variable | {imagepath} |
| :--- | :--- |
| Sample value: | /opt/digiverso/goobi/metadata/27/images |
| Meaning: | The absolute path to the image folder for the process. This is a subfolder of {processpath}. It contains various folders for each item of digitised material. |

### Static variable: {tifpath}

| Variable: | {tifpath} |
| :--- | :--- |
| Sample value: | /opt/digiverso/goobi/metadata/27/images/kleiuniv_PPN517154005_media |
| Meaning: | The absolute path to the media folder for the process. This is a subfolder of {imagepath}. It contains the optimised digital images. This folder is usually exported at the end of the workflow. |

### Static variable: {origpath}

| Variable: | {origpath} |
| :--- | :--- |
| Sample value: | /opt/digiverso/goobi/metadata/27/images/master_kleiuniv_PPN517154005_media |
| Meaning: | The absolute path to the media folder for the process. This is a subfolder of {imagepath}. It contains the scanned images. Derivatives for other folders are usually generated from this folder. |

### Static variable: {metaFile}

| Variable: | {metaFile} |
| :--- | :--- |
| Sample value: | /opt/digiverso/goobi/metadata/27/meta.xml |
| Meaning: | The absolute path to the metadata file in Goobi. This file can be present in a range of formats. |

### Static variable: {tifurl}

| Variable: | {tifurl} |
| :--- | :--- |
| Sample value: | [file:///opt/digiverso/goobi/metadata/27/images/kleiuniv_PPN517154005_media](file:///opt/digiverso/goobi/metadata/27/images/kleiuniv_PPN517154005_media) |
| Meaning: | The path for {tifpath} as a valid URL. |

### Static variable: {origurl}

| Variable: | {origurl} |
| :--- | :--- |
| Sample value: | [file:///opt/digiverso/goobi/metadata/27/images/master_kleiuniv_PPN517154005_media](file:///opt/digiverso/goobi/metadata/27/images/master_kleiuniv_PPN517154005_media) |
| Meaning: | The path for {origpath} as a valid URL. |

### Static variable: {sourcepath}

| Variable: | {sourcepath} |
| :--- | :--- |
| Sample value: | /opt/digiverso/goobi/metadata/27/images/kleiuniv_PPN517154005_source/ |
| Meaning: | The path to the source folder for the process. This folder can be used to store files that are to be included in exports to the Goobi viewer. |

### Static variable: {projectid}

| Variable: | {projectid} |
| :--- | :--- |
| Sample value: | 4 |
| Meaning: | The internal ID of the project within the Goobi workflow database. |

### Static variable: {projectname}

| Variable: | {projectname} |
| :--- | :--- |
| Sample value: | Monographs 1850-1950 |
| Meaning: | The name of the project within the Goobi workflow database. |

### Static variable: {projectidentifier}

| Variable: | {projectidentifier} |
| :--- | :--- |
| Sample value: | M1850-1950 |
| Meaning: | The speaking identifier that was additionally given to the project independent of the database ID. |

### Static variable: {iiifMediaFolder}

| Variable: | {iiifMediaFolder} |
| :--- | :--- |
| Sample value: | "[http://example.com/goobi/api/process/image/12345/schudiss_618299084_media/00000001.tif/full/max/0/default.jpg?jwt=1234567890](http://example.com/goobi/api/process/image/12345/schudiss_618299084_media/00000001.tif/full/max/0/default.jpg?jwt=1234567890)", "[http://example.com/goobi/api/process/image/12345/schudiss_618299084_media/00000002.tif/full/max/0/default.jpg?jwt=0987654321](http://example.com/goobi/api/process/image/12345/schudiss_618299084_media/00000002.tif/full/max/0/default.jpg?jwt=0987654321)", ... |
| Meaning: | Listing of IIIF URLs to all images from the `media` directory of a process |

### Static variable: {iiifMasterFolder}

| Variable: | {iiifMasterFolder} |
| :--- | :--- |
| Sample value: | "[http://example.com/goobi/api/process/image/12345/schudiss_618299084_master/00000001.tif/full/max/0/default.jpg?jwt=1234567890](http://example.com/goobi/api/process/image/12345/schudiss_618299084_master/00000001.tif/full/max/0/default.jpg?jwt=1234567890)", "[http://example.com/goobi/api/process/image/12345/schudiss_618299084_master/00000002.tif/full/max/0/default.jpg?jwt=0987654321](http://example.com/goobi/api/process/image/12345/schudiss_618299084_master/00000002.tif/full/max/0/default.jpg?jwt=0987654321)", ... |
| Meaning: | Listing of IIIF URLs to all images from the `master` directory of a process |

## Dynamic variables

As well as static variables, there is a range of dynamic variables that can be used to access all the freely configurable data in Goobi.

### Dynamic variable: {process.NAME}

| Variable: | {process.NAME} |
| :--- | :--- |
| Example: | {process.b-number} |
| Sample value: | b20057465 |
| Meaning: | This variable can be used to access the value of every process attribute. |

### Dynamic variable: {product.NAME}

| Variable: | {product.NAME} |
| :--- | :--- |
| Example: | {product.Artist} |
| Sample value: | Niedersächsische Staats- und Universitätsbibliothek Göttingen, Germany |
| Meaning: | This variable can be used to access the value of every workpiece attribute. |

### Dynamic variable: {template.NAME}

| Variable: | {template.NAME} |
| :--- | :--- |
| Example: | {template.Shelfmark} |
| Sample value: | 8 HLP II, 8726 |
| Meaning: | This variable can be used to access the value of every template attribute. |

### Dynamic variable: {meta.NAME}

| Variable: | {meta.NAME} |
| :--- | :--- |
| Example: | {meta.PlaceOfPublication} |
| Sample value: | Göttingen |
| Meaning: | This variable allows you to use the value of an item of metadata. The metadata file is searched recursively, and the first value found is used. |

### Dynamic variable: {meta.topstruct.NAME}

| Variable: | {meta.topstruct.NAME} |
| :--- | :--- |
| Example: | {meta.topstruct.CatalogId Digital} |
| Sample value: | 517154005 |
| Meaning: | This variable allows you to use the value of an item of metadata. Only the highest structure element is searched for the metadata. |

### Dynamic variable: {meta.firstchild.NAME}

| Variable: | {meta.firstchild.NAME} |
| :--- | :--- |
| Example: | {meta.firstchild.CurrentNo} |
| Sample value: | 12 |
| Meaning: | This variable allows you to use the value of an item of metadata located in the first sub-element of the main element. This is particularly useful in the case of multi-volume or periodical structures. |

### Dynamic variable: {db_meta.NAME}

| Variable: | {db_meta.NAME} |
| :--- | :--- |
| Example: | {db_meta.DocStruct} |
| Sample value: | Monograph |
| Meaning: | With this variable the value of a metadata can be used. This is not read from the METS file itself in this case, but instead comes from the cached version from the database. |

### Dynamic variable: {datetime.PATTERN}

| variable: | {datetime.PATTERN} |
| :--- | :--- |
| Example: | {datetime.yyyy-MM-dd} |
| Example value: | 2024-08-13 |
| Meaning: | This variable can be used to generate the current date and time in any format. The format `PATTERN` can contain all permitted symbols for date and time formatting in Java. You can find more information on this at: https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html |