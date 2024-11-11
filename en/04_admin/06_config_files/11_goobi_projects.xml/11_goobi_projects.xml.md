# goobi_projects.xml

The file `goobi_projects.xml` configures the mask for creating processes. Here it is defined per project which metadata and properties are allowed for certain publication types.

The file is usually located at the following location:

```bash
/opt/digiverso/goobi/config/goobi_projects.xml
```

For example, this configuration file looks like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<goobiProjects>

    <project name="default">
        <name>Example project</name>
        <name>Sample.*</name>
        <createNewProcess>
            <itemlist>
                <!-- Title for all -->
                <item docstruct="topstruct" from="vorlage" isnotdoctype="multivolume" metadata="TitleDocMain" required="true" ughbinding="true"> Title </item>
                <item docstruct="topstruct" from="vorlage" isnotdoctype="multivolume" metadata="TitleDocMainShort" required="true" ughbinding="true"> Sorting title</item>
                <!-- Title just for the Multivolume -->
                <item docstruct="topstruct" from="vorlage" isdoctype="multivolume" metadata="TitleDocMain" required="true" ughbinding="true"> Title </item>
                <item docstruct="topstruct" from="vorlage" isdoctype="multivolume" metadata="TitleDocMainShort" required="true" ughbinding="true"> Sorting title</item>
                <!-- Authors and Creators -->
                <item docstruct="topstruct" from="vorlage" isdoctype="monograph\|multivolume\|periodical" ughbinding="false">Authors</item>
                <!-- Identifer -->
                <item docstruct="topstruct" from="werk" isnotdoctype="periodical" ughbinding="false">ATS</item>
                <item docstruct="topstruct" from="werk" isdoctype="periodical" ughbinding="false">TSL</item>
                <item docstruct="topstruct" from="werk" isdoctype="multivolume" metadata="CatalogIDDigital" required="true" ughbinding="true">Identifier set</item>
                <item docstruct="topstruct" from="werk" isdoctype="monograph" metadata="CatalogIDDigital" required="true" ughbinding="true"> Identifier monograph</item>
                <item docstruct="topstruct" from="werk" isdoctype="periodical" metadata="CatalogIDDigital" required="true" ughbinding="true"> Identifier journal</item>
                <item docstruct="topstruct" from="werk" isdoctype="periodical" metadata="ISSN" required="true" ughbinding="true"> ISSN </item>
                <item docstruct="firstchild" from="werk" isdoctype="multivolume\|periodical" metadata="CatalogIDDigital" required="true" ughbinding="true">Identifier volume </item>
                <!-- Title, number and authors for Multivolumes and Periodicals -->
                <item docstruct="firstchild" from="vorlage" isdoctype="multivolume\|periodical" metadata="TitleDocMain" required="true" ughbinding="true"> Title (volume)</item>
                <item docstruct="firstchild" from="vorlage" isdoctype="multivolume\|periodical" metadata="TitleDocMainShort" required="true" ughbinding="true"> Sorting title (volume)</item>
                <item docstruct="firstchild" from="vorlage" isdoctype="multivolume" ughbinding="false"> Authors (volume)</item>
                <item docstruct="firstchild" from="vorlage" isnotdoctype="monograph" metadata="CurrentNo" ughbinding="true"> Volume number </item>
                <item docstruct="firstchild" from="vorlage" isnotdoctype="monograph" metadata="CurrentNoSorting" ughbinding="true"> Sorting number</item>
                <!-- Other metadata for all -->
                <item docstruct="topstruct" from="vorlage" isdoctype="monograph\|multivolume\|periodical" metadata="PlaceOfPublication" ughbinding="true"> Publishing place </item>
                <item docstruct="topstruct" from="vorlage" isdoctype="monograph" metadata="PublicationYear" ughbinding="true"> Publishing year </item>
                <item docstruct="firstchild" from="vorlage" isdoctype="periodical\|multivolume" metadata="PublicationYear" ughbinding="true">Publishing year </item>
                <item docstruct="firstchild" from="vorlage" isdoctype="multivolume\|periodical" metadata="PublisherName" ughbinding="true"> Publishing house </item>
                <item docstruct="topstruct" from="vorlage" isdoctype="monograph" metadata="PublisherName" ughbinding="true"> Publishing house </item>
                <item from="vorlage" isdoctype="periodical\|multivolume" ughbinding="true" docstruct="firstchild" metadata="shelfmarksource"> Shelfmark </item>
                <item from="vorlage" isdoctype="monograph\|map\|manuscript" ughbinding="true" docstruct="topstruct" metadata="shelfmarksource"> Shelfmark </item>
                <!--dropdown to select the font type -->
                <item docstruct="topstruct" from="prozess" multiselect="false" metadata="FontType" required="true" ughbinding="true">
                    Font type
                    <select label="Antiqua">Antiqua </select>
                    <select label="Gothic">Gothic</select>
                    <select label="Mixed">Mixed </select>
                </item>
                <!-- Hidden fields: dropdown fields with only one value -->
                <item docstruct="topstruct" isnotdoctype="periodical\|multivolume" metadata="_dateDigitization" multiselect="true" required="true" ughbinding="true">
                    Digitisation date
                    <select label="2021"> 2021 </select>
                </item>
                <item docstruct="firstchild" isdoctype="periodical\|multivolume" metadata="_dateDigitization" multiselect="true" required="true" ughbinding="true">
                    Digitisation date
                    <select label="2021"> 2021</select>
                </item>
                <item docstruct="topstruct" from="vorlage" metadata="PhysicalLocation" multiselect="true" required="true" ughbinding="true">
                    Physical location
                    <select label="Berlin"> Berlin </select>
                    <select label="Göttingen"> Göttingen </select>                    
                </item>
                <processtitle isnotdoctype="monograph">ATS+TSL+'_'+Identifier volume+'_'+Volume number</processtitle>
                <processtitle isdoctype="monograph" replacewith="_">ATS+TSL+'_'+Identifier monograph</processtitle>
                <hide>collections</hide>
            </itemlist>
            <opac use="true">
                <catalogue>K10Plus</catalogue>
            </opac>
            <templates use="false" />
            <defaultdoctype>monograph</defaultdoctype>
            <metadatageneration use="true" />
            <fileupload use="true">
                <folder regex="/^.*$/" messageKey="uploadFileErrorIntern">intern</folder>
            	<folder regex="/^.*\\.(jpg\|jpeg\|png\|tif\|jp2)$/" messageKey="uploadFileErrorMaster">master</folder>
                <folder regex="/^.*\\.jpg$/" messageKey="uploadFileErrorMedia">media</folder>
                <folder regex="/^.*\\.pdf$/" messageKey="uploadFileErrorExport">export</folder>
            </fileupload>     
        </createNewProcess>
        <tifheader>
            <monograph>'|[[TYPE]]'+$Doctype+'|[[TITLE]]'+Title+'|[[AUTHORS]]'+Authors+'
                |[[YEAR]]'+Publishing year+'|[[PLACE]]'+Publishing place+'|[[FOLDER]]'+ATS+'_'+Identifier monograph+'|'
            </monograph>
            <multivolume>'|[[TYPE]]'+$Doctype+'|[[TITLE]]'+Title+'|[[AUTHORS]]'+Authors+'
                |[[YEAR]]'+Publishing year+'|[[PLACE]]'+Publishing place+'|[[FOLDER]]'+ATS+'_'+Identifier volume+'_'+Label number+'|'
            </multivolume>
            <periodical>'|[[TYPE]]'+$Doctype+'|[[TITLE]]'+Title+'|[[AUTHORS]]'+Authors+'
                |[[YEAR]]'+Publishing year+'|[[PLACE]]'+Publishing place+'|[[FOLDER]]'+TSL+'_'+Identifier volume+'_'+Label number+'|'
            </periodical>
        </tifheader>
        <dmsImport />
        <validate>
        	<metadata createelementfrom="" docstruct="" metadata="">
        		Create CreatorsAllOrigin
        	</metadata>
        </validate>
    </project>
</goobiProjects>
```

## Definition of the projects

For each project a `<project>` element can be created. The name of the project is specified either with the `name` parameter or with the `<name>` sub-element. If a configuration is to apply to projects with different names, multiple `<name>` elements can be specified. Alternatively, a regex expression can be used instead of the name to address multiple projects. The default project configuration should always be a project named `default`. When a project is created in Goobi Workflow, a suitable configuration is searched for according to the following sequence:

1. search for the first `project` entry whose name matches or contains the project name
2. search for a `project` entry whose name, interpreted as a regular expression, matches the project name
3. search for a `project` entry with the name `default
4. use the first `project` entry

## Project details

The sub-elements of `<project>` contain a number of details that are taken into account when loading the creation mask for tasks in the user interface.

### Properties of a new process

All details around the input fields that are important for loading the creation mask are specified in the `<createNewProcess>` element. This includes in particular the `<itemlist>` element where the input fields are listed.

#### List of the input fields

Each input field in the user interface is described by an `<item>` in this list. These entries can be used to add text fields and dropdown menus. More specific fields, such as a file upload area, are described below.

Each `<item>` element contains as content the text that is displayed in the label column in the input mask table. This can additionally be translated into different languages by Goobi Workflow's translation mechanism using the messages files.

An `<item>` is displayed either as a text field or as a drop-down menu. The following parameters apply to both types of input fields:

| Attribute | Possible values | Meaning |
| :--- | :--- | :--- |
| `docstruct` | `topstruct`, `firstchild` | The `docstruct` attribute can contain two allowed values: `topstruct` and `firstchild`. As with other configurations, these specify whether the defined metadata should be stored for the topmost structure element or to the child element. |
| `from` | `werk`, `vorlage`, `prozess` | The `from` attribute can be used to create the value as a property. The allowed values work, template and process control whether this is a template property, workpiece property or process property. |
| `isdoctype` | Publication type | The `isdoctype` attribute can be used to control for which publication types a metadatum is to be displayed. The publication type names used here must have been defined in the `goobi_opac.xml` file. |
| `isnotdoctype` | Publication type | The `isnotdoctype` attribute can be used to control for which publication types a metadate should not be displayed. This attribute can be used if an input field matches all but one specific document type. The publication type names used here must have been defined in the `goobi_opac.xml` file. |
| `required` | `true`, `false` | If `required` is set to `true`, then the entry field is marked as mandatory in the user interface. If such a field is left blank when filling out the form, Goobi will notify the user and the creation process will not be able to be completed. |
| `initStart` | Text | By `initStart` a static prefix can be added. Furthermore, the contained value can be generated automatically. This setting makes sense especially for identifiers. |
| `initEnd` | Text | By `initEnd` a static suffix can be added. Furthermore, the contained value can be generated automatically. This setting makes sense especially for identifiers. |
| `ughbinding` | `true`, `false` | If `ughbinding="true"` is specified, the value of the property or metadatum will be filled by the result of the OPAC query. |
| `metadata` | `MetadataType` | If the `metadata` attribute is specified, not only a property is defined here, but also a metadata of the specified type in the associated METS file. The value specified here must match a metadata definition in the rule set used. |
| `autogenerated` | `true`, `false` | This parameter can be used to specify whether the field should be automatically filled with an identifier if it has no content. |

##### Dropdown menus

As soon as an `<item>` contains the `multiselect` parameter and sub-items `<select>`, it will no longer be displayed as a text field but as a dropdown menu. The `multiselect` parameter can be set to `true` or `false` to allow or disallow the selection of multiple items.

Each `<select>` element can have a `label` parameter. The `label` text is displayed in the menu while the content of the `<select>` element is technically processed. This allows to specify a more readable alternative name for the display.

Even an `<item>` that is displayed as a dropdown menu needs a label. This is specified in parallel to the `<select>` elements.

For example, if a city abbreviation is to be selectable when creating an operation, it would be useful for users to have the spelled out names displayed in the menu:

```xml
<item multiselect="false" required="true">
    Physical location
    <select label="Berlin">B</select>
    <select label="Göttingen">GOE</select>                    
    <select label="Hannover">H</select>                    
</item>
```

##### Hiding input fields

The `<hide>` element can be used to hide input fields, i.e. `<item>` elements defined here. The field can contain for example the following values: `collections`, `doctype`, `preferences`, `images` and `processtitle`.

The collection selection can be hidden using `collections`, `doctype` controls the display of the field for selecting the document type, `preferences` the selection field for the ruleset, `images` the input for the expected number of digitised pages and `processtitle` the display of the generated process title.

##### Process title

If the process title is to be generated automatically, the `<processTitle>` element can be used to specify formation rules for the titles. Process titles can be generated differently for certain document types. To assign a document type to an education rule, the `isdoctype` parameter is used. Alternatively, all document types can be used and only a specific type can be excluded with the `isnotdoctype` parameter.

Between the start and end elements of `<processTitle>` is an expression describing the title to be generated. Text passages are written in single quotes and as variable names all properties defined above can be used. All elements are concatenated with the `+` operator.

For example, to generate a title for all documents that are not `periodical` that includes the author and the title of the document, the following entry would be useful:

```xml
<processTitle isnotdoctype"periodical">Author + '_' + Title</processTitle>
```

The `replacewith` parameter can be used to specify a string to replace all invalid letters and special characters in the automatically generated operation title, if required. If the string is `""`, all invalid characters will be removed. Even if this parameter is missing, all special characters will be removed without replacement.

#### OPAC catalog selection

The OPAC catalog query can be activated by setting the `use` attribute to the value `true` within the `<opac>` parameter. The preselected catalog can be defined in the `<catalogue>` sub-element. If the value is not set or does not correspond to any entry from the `goobi_opac.xml` file, the first catalog defined there will be used as default value.

#### Using other operations as templates

To import the metadata from already existing operations, the `use` attribute in the `<templates>` element must be set to the `true` value. This makes the `Select from existing tasks` option available, which lists all tasks for which the `Display in selection list` checkbox was activated during creation.

#### Default document type

The publication type selected when opening the creation mask can be defined in the field `<defaultdoctype>`. The name used here comes from the `doctypes` definition of the configuration file `goobi_opac.xml`.

#### Metadata generation

By using the `<metadatageneration />` element with the `use="true"` parameter, additional metadata can be automatically generated when an operation is created.

#### Uploading files

With the configuration of `<fileupload>` the upload area can be enabled. With this, files can already be uploaded to the newly created task. Which folders are available for selection can be configured in the subfield `<folder>`.

The `regex` parameter can be used to specify which file names are accepted by the upload button in the user interface. If the file selected by the user does not match the regex expression, the file will not be uploaded and an error message will be displayed. If the regex parameter is omitted or an empty string is specified, files of all file types and names are uploadable. Since the regex expression is evaluated by Primefaces, it must be enclosed in slashes:

Valid notation:

`/^.*\.pdf$/`

Invalid notation:

`^.*\.pdf$`

The `messageKey` parameter specifies a key which can be used in `messages_xx.properties` files to store individual error messages. For example, if a file upload is restricted to PDF files as shown above, then an error message indicating an incorrect file type can be specified in the messages files in all languages under the key specified here. If the parameter is omitted or the key is not found, a standard error message is displayed.

### Tiff header

In the `<tifheader>` element, values can be specified that are to be written to the tiff headers. Here, a separate text can be defined for each publication type previously defined in a `<item>`.

For example, if a `<item>monograph</item>` has been defined, the following can be entered here:

```xml
<monograph>'|DOC_TYPE'+$Doctype+'|MAINTITLE'+Title+'|AUTHORS/PUBLISHER'+Authors+'YEAR'+PublicationYear+'|PUBLICATION LOCATION'+PublicationLocation+'|'</monograph>
```

### Import from DMS

To import data from a document management system, the `<dmsImport>` element can be specified.

### Validation

Data of the form can be validated. Validations can be specified in the `<validate>` element.