# goobi_opac.xml

The configuration file `goobi_opac.xml` defines the communication between Goobi workflow and external data sources. This usually applies to systems such as library catalogs. The file is usually located at the following storage path:

```bash
/opt/digiverso/goobi/config/goobi_opac.xml
```

For example, this configuration file looks as follows:

{% code title="goobi_opac.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<opacCatalogues>
    <doctypes>
        <type title="monograph" isContainedWork="false" isMultiVolume="false" isPeriodical="false" rulesetType="Monograph" rulesetChildType="Special Monograph" tifHeaderType="Monographie">
            <label language="de">Monographie</label>
            <label language="en">Monograph</label>
            <mapping>Aa</mapping>
            <mapping>Oa</mapping>
            <mapping>Monograph</mapping>
        </type>
        <type title="periodical" isContainedWork="false" isMultiVolume="false" isPeriodical="true" rulesetType="Periodical" rulesetChildType="PeriodicalVolume" tifHeaderType="Band_Zeitschrift">
            <label language="de">Zeitschrift</label>
            <label language="en">Periodical</label>
            <mapping>Ab</mapping>
            <mapping>Ob</mapping>
            <mapping>Periodical</mapping>
        </type>
        <type title="multivolume" isContainedWork="false" isMultiVolume="true" isPeriodical="false" rulesetType="MultivolumeWork" rulesetChildType="Volume" tifHeaderType="Band_MultivolumeWork">
            <label language="de">Mehrbändiges Werk</label>
            <label language="en">Multivolume work</label>
            <mapping>Of</mapping>
            <mapping>Af</mapping>
            <mapping>OF</mapping>
            <mapping>AF</mapping>
            <mapping>MultiVolumeWork</mapping>
        </type>
    </doctypes>
    <catalogue title="K10Plus">
        <config opacType="PICA" description="K10plus" protocol="http://" address="kxp.k10plus.de" port="80" database="2.1" charset="UTF-8" iktlist="IKTLIST-GBV.xml" ucnf="UCNF=NFC&amp;XPNOFF=1" />
        <searchFields>
            <searchField label="LCCN" value="12" />
            <searchField label="ISBN" value="7" />
            <searchField label="ISSN" value="8" />
        </searchFields>
		<specialmapping type="multivolume" />k10_multivolume</specialmapping>
		<specialmapping type="periodical" />k10_periodical</specialmapping>
    </catalogue>
    <catalogue title="Library of Congress">
        <config opacType="GBV-MARC" description="Library of Congress SRU (Voyager)" address="http://opac.intranda.com/sru/DB=1" port="80" database="1" iktlist="IKTLIST.xml" ucnf="XPNOFF=1" />
        <searchFields>
            <searchField label="LCCN" value="12" />
            <searchField label="ISBN" value="7" />
            <searchField label="ISSN" value="8" />
        </searchFields>
    </catalogue>
    <catalogue title="UBBI">
        <config opacType="ALMA-MARC" description="Katalog UB Bielefeld" address="https://hbz-ubbi.alma.exlibrisgroup.com/view/sru/49HBZ_BIE" port="80" database="1" iktlist="IKTLIST.xml" ucnf="XPNOFF=1" />
        <searchFields>
            <searchField label="HBZHT" value="alma.other_system_number_035_a_exact"/>
            <searchField label="MMS ID" value="mms_id"/>
            <searchField label="ISBN" value="alma.isbn"/>
            <searchField label="ISSN" value="alma.issn"/>
        </searchFields>
        <beautify>
            <setvalue tag="tag1" subtag="21" value="a">
                <condition tag="tag2" subtag="22" value="s" />
          	</setvalue>
 			<setvalue tag="tag3" subtag="33" value="m">
                <condition tag="tag4" subtag="33" value="s" />
            </setvalue>
		</beautify>
    </catalogue>
</opacCatalogues>
```
{% endcode %}

## Publication types

Several publication types can be defined in the `<doctypes>` element. Each type is in its own `<type>` element and has some properties specified by parameters and subelements.

### Properties of a publication type

All important properties of a publication type are specified as parameters in the `<type>` element. The following parameters can be used:

| Attribute | Possible Values | Meaning |
| :--- | :--- | :--- |
| `title` | Text | This field specifies the title of the publication type. The title is a technically easy-to-use name that can be translated with the `<label>` subelement. |
| `isContainedWork` | `true`, `false` | This value can be set to `true` if this publication type is a part of another publication type. For example, this can be used if there are removable maps in a book and this publication type represents the maps that are included. **Note:** This parameter is largely deprecated and should no longer be used. |
| `isMultiVolume` | `true`, `false` | This value can be set to `true` if the publication type is a multi-volume edition, for example a single volume of an encyclopedia. |
| `isPeriodical` | `true`, `false` | This value can be set to `true` if the publication type is a regular edition, for example a newspaper. |
| `rulesetType` | Name from `ruleset.xml` | This field can be used to specify a rule set to be associated with this publication type. |
| `rulesetChildType` | Name from `ruleset.xml` | This field can be used to specify a rule set sub-element to be associated with this publication type. |
| `tifHeaderType` | Text | This field can be used to specify a label to be written in the file header when exporting to tiff files. |

### Translation of titles

The name of a publication type specified in the `title` parameter is used internally in the software and is therefore not always easily readable by users and is not translated automatically. Therefore, the publication type name can be translated into different languages using the `<label>` element. The `language` parameter specifies the language abbreviation. Depending on the configuration, the following languages are usually supported:

```xml
<type title="periodical">
    <label language="de">German translation</label>
    <label language="en">English translation</label>
    <label language="es">Spanish translation</label>
    <label language="fr">French translation</label>
    <label language="it">Italian translation</label>
    <label language="iw">Hebrew translation</label>
    <label language="nl">Dutch translation</label>
    <label language="pt">Portuguese translation</label>
</type>
```

### Mapping to other data formats

It can happen that a publication type should be able to be found with a search function or with external data formats via certain designations or abbreviations that cannot be derived from the title. For this purpose, further designations can be specified for each type with the sub-element `<mapping>id42</mapping>`. If then, for example, the ID `id42` is searched for, the corresponding publication type will be found.

## Catalogues

Goobi can use metadata from different catalogs. These are entered with the `<catalogue>` element directly in the `<opacCatalogues>` element. For each catalog element, the `title` parameter specifies the official name of the respective catalog.

### Configuration of a catalogue

Some other properties of a catalog are specified as parameters in the `<config>` subelement. The following parameters can be used:

| Attribute | Possible Values | Meaning |
| :--- | :--- | :--- |
| `opacType` | OPAC-Type | This parameter can be used to specify the OPAC type of the database used by the catalog. For example, this can be `PICA`, `ALMA-MARC` or `GBV-MARC`. |
| `description` | Text | A description of the catalog can be specified here. |
| `protocol` | Protocol | This parameter is usually set to `http://` or `https://` if the protocol is not already included in the `address` parameter. |
| `address` | URL | This parameter specifies the domain name or IP address of the catalog service API. If the network protocol is specified here, the `protocol` parameter must be left empty. |
| `port` | Port number | The port number can be used to specify a particular network port of the catalog service API. Usually this is the default HTTP port `80`. |
| `database` | Number | This parameter can be used to specify the database version to be used for API requests. |
| `charset` | Charset | This parameter can be used to specify a character set with which the database should return the records. |
| `iktlist` | File path | This parameter is used only if the catalogue uses a PICA database. The filename must refer to an IKTLIST file that provides information about media numbering systems. |
| `ucnf` | Text | This parameter is used to insert UCNF information into the URL of the API request. |

### Search options

Metadata is identified in catalogs using specific numbers (for example ISBN or ISSN). If metadata is to be imported into Goobi using a given number from the respective catalogue, the `<searchFields> element can be used to list different numbering systems. A user can then enter an ISBN number in the following example and select the ISBN field to match it:

```xml
<searchFields>
    <searchField label="LCCN" value="12" />
    <searchField label="ISBN" value="7" />
    <searchField label="ISSN" value="8" />
</searchFields>
```

Each `<searchField>` element represents an option in the corresponding dropdown menu. The text specified in `label` is displayed on the user interface. The value defined in `value` is the internal ID of the numbering system. Depending on the catalog, a text-based ID can also be used. This can look like this, for example:

```xml
<searchField label="ISBN" value="alma.isbn"/>
<searchField label="ISSN" value="alma.issn"/>
```

Detailed information about supported numbering systems can be retrieved from the respective catalogue API. This is an XML file that can be called directly in the browser. The domain must be adapted according to the used provider.

```xml
https://opac.intranda.com/XML=1.0/IKTLIST
https://kxp.k10plus.de/XML=1.0/IKTLIST
```

### Mapping to publication types

As described above, publication types can be found with alternative labels. In addition, it is possible in `<catalogue>` elements to link catalogue-specific designations (and thus also catalogues) to publication types using the `<specialmapping>` element. Thus, matching publication types can be defined and found via the alternative designations of a catalogue.

The `type` parameter of the `<specialmapping>` element refers to the `title` of the previously defined publication type. The `<specialmapping>` element contains an alternative name. The following example would link the search term `k10plus_periodical` to the publication type `periodical` for a K10Plus catalogue:

```xml
<doctypes>
    <type title="periodical">
    ...
    </type>
</doctypes>
...
<catalog title="K10Plus">
    <specialmapping type="periodical">k10plus_periodical</specialmapping>
</catalog>
```

### Customizing records from MARC files

If records are retrieved from catalogs, they are imported into Goobi via MARC files, among others. Records from these files can be customized using certain replacement patterns. For this purpose, the `<beautify>` element is used as a direct sub-element of the corresponding `<catalogue>` element and can contain any number of `<setvalue>` commands.

Since processing MARC data with these commands can become very complex, only a few simple examples are described here based on the following MARC data excerpt.

```xml
...
<datafield tag="book" ind1="" ind2="">
    <subfield code="author">Alice April</subfield>
    <subfield code="title">Garden tips</subfield>
    <subfield code="year">1930</subfield>
    <subfield code="other_id">aaa01</subfield>
</datafield>
<datafield tag="book" ind1="" ind2="">
    <subfield code="author">John Doe</subfield>
    <subfield code="title">The small world</subfield>
    <subfield code="year">1920</subfield>
    <subfield code="other_id">aaa02</subfield>
</datafield>
<datafield tag="paper" ind1="" ind2="">
    <subfield code="author">Dr. Arthur Williams</subfield>
    <subfield code="title">Complex numbers</subfield>
    <subfield code="year">1910</subfield>
    <subfield code="other_id">aaa03</subfield>
</datafield>
...
```

The following command can be used to replace certain values. For example, if it turns out that some records of type `book` have an invalid year (`year`), incorrect data can be corrected. The `setvalue` command specifies that in each `datafield` with tag `book` addressed with the inner `<condition>`, the `subfield` with parameter `code="year"` should get the value `1900`. The `<condition>` says that all `datafield` elements should be considered which have the tag `book` and where a subelement with `code="year"` and the value `190` exists.

```xml
<beautify>
    <setvalue tag="book" subtag="year" value="1900">
        <condition tag="book" subtag="year" value="190" />
    </setvalue>
</beautify>
```

Data can be filtered with the `<setvalue>` command. For example, if you want to remove the `other_id` elements, their value can be overwritten with an empty string.

**Note:** An asterisk (*) is a placeholder for an arbitrary value. Regular expressions are not supported.

```xml
<beautify>
    <setvalue tag="*" subtag="other_id" value="">
        <condition tag="*" subtag="other_id" value="*" />
    </setvalue>
</beautify>
```

Data sets can also be supplemented with new properties. However, this works only conditionally, because only the data from the MARC file and from the `<setvalue>` command can be accessed. For example, it is possible to assign new tags to records with certain contents:

```xml
<beautify>
    <setvalue tag="paper" subtag="target_group" value="students">
        <condition tag="paper" subtag="author" value="Dr. Arthur Williams" />
    </setvalue>
</beautify>
```

{% hint style="info" %}
**Note:**\
Please note that Goobi was originally designed for communication with PICA catalogs. Many other catalog systems are now also supported. However, these often require a very individual configuration, e.g. for communication via the Z39.50 protocol or using SRU.
{% endhint %}