# goobi_metadataDisplayRules.xml

The `goobi_metadataDisplayRules.xml` configuration file specifies how the metadata is to be displayed within Goobi's metadata editor. It is usually located at the following path in the file system.

```bash
/opt/digiverso/goobi/config/goobi_metadataDisplayRules.xml
```

This configuration file describes how individual metadata fields are to be displayed. Among other things, it can be specified that fields are displayed as input fields, selection lists, read-only fields, etc., and can be edited differently by the user. Here is an example of such a configuration file:

{% code title="goobi_metadataDisplayRules.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<displayRules>
    <ruleSet>
        <context projectName="*">
            
            <!-- text field -->
            <textarea ref="TitleDocMain">
                <label></label>
            </textarea> 
             <input ref="CatalogIDSource">
                <label></label>
            </input> 
            
            <!-- text area -->
            <textarea ref="TitleDocMainShort">
                <label></label>
            </textarea> 
            <textarea ref="Description">
                <label></label>
            </textarea> 
            
            <!-- default value -->
            <input ref="PlaceOfPublication">
                <label>Göttingen</label>
            </input> 
            
            <!-- read only -->
            <readonly ref="CatalogIDDigital">
                <label></label>
            </readonly>
            
            <!-- Single select -->
            <select1 ref="singleDigCollection">
                <item selected="true">
                    <label>General</label>
                    <value>General</value>
                </item>

                <item selected="false">
                    <label>Biology</label>
                    <value>Biology</value>
                </item>

                <item selected="false">
                    <label>Physics</label>
                    <value>Physics</value>
                </item>

                <item selected="false">
                    <label>Mathematics</label>
                    <value>Mathematics</value>
                </item>
            </select1>
            
            <!-- Multi select  -->
            <select ref="Classification">
                <item selected="true">
                    <label>Blue</label>
                    <value>Blue</value>
                </item>

                <item selected="false">
                    <label>Red</label>
                    <value>Red</value>
                </item>

                <item selected="false">
                    <label>Green</label>
                    <value>Green 2</value>
                </item>

                <item selected="false">
                    <label>Yellow</label>
                    <value>Yellow</value>
                </item>
            </select>

        </context>
    </ruleSet>
</displayRules>
```
{% endcode %}

In this configuration file, you can define within the `projectName` attribute for which projects this individually configured display is to apply.

The IDs specified with `ref` refer to the metadata names that exist in the database for the corresponding project (or task).

Most elements have a child elements `label`. This can contain text to describe the input field. Normally, this is the name of the concerning meta data, but it can be different for better readability.

In addition, different field types can be selected from a list:
<!--- This list is based on the enum org.goobi.api.display.enums.DisplayType -->

## Input Box

The `input` box is displayed as a normal single-line input field.

```xml
<input ref="PlaceOfPublication">
    <label>Göttingen</label>
</input>
```

## Text Area

The type `textarea` is similar to the Input Box. However, it is multiline and allows the display size of the field to be adjusted.

```xml
<textarea ref="TitleDocMain">
    <label />
</textarea>
```

## Read only Field

The type `readonly` is similar to the Input Box, but it does not allow changing the field content. 

```xml
<readonly ref="CatalogIDDigital">
    <label />
</readonly>
```

## Select Box

The select box `select1` allows the selection of **one** value from a list of values. A distinction is made between the display of the value (`label`) and the actual value to be stored internally (`value`). With the `selected` parameter, **one** `<item>` element can be preselected.

```xml
<select1 ref="singleDigCollection">
    <item selected="true">
        <label>Default</label>
        <value>DefaultCollection</value>
    </item>
    <item selected="false">
        <label>Biology</label>
        <value>Biology</value>
    </item>
    <item selected="false">
        <label>Physics</label>
        <value>Physics</value>
    </item>
    <item selected="false">
        <label>Mathematics</label>
        <value>Mathematics</value>
    </item>
</select1>
```

## Multi Select Box

The Multi Select Box `select` allows you to select **multiple** values, all of which should be stored within the metadata field. Here, too, a distinction is made between the displayed value (`label`) and the internally stored value (`value`). With the `selected` parameter, **multiple** `<item>` elements can be preselected.

```xml
<select ref="Classification">
    <item selected="true">
        <label>Default classification</label>
        <value>DefaultClassification</value>
    </item>
    <item selected="false">
        <label>Classification 1</label>
        <value>Classification 1</value>
    </item>
    <item selected="false">
        <label>Classification 2</label>
        <value>Classification 2</value>
    </item>
    <item selected="false">
        <label>Classification 3</label>
        <value>Classification 3</value>
    </item>
</select>
```

## HTML Input

The `htmlInput` field type allows you to enter texts with optical formatting options. For example, text can be marked in bold or italic and is saved in the METS file along with the formatting.

```xml
<htmlInput ref="Description">
    <label></label>
</htmlInput>
```

## GeoNames

The `geonames` type allows the search and selection of locations within the GeoNames database.

```xml
<!-- Geonames as selectable field, in ruleset the PlaceOfPublication has to have this attribute then: normdata="true" -->
<geonames ref="PlaceOfPublication">
    <label></label>
</geonames>
```

## GND

The field type `gnd` allows the search and data transfer of entries from the Common Standards Database of the German National Library.

```xml
<gnd ref="Subject">
    <label />
</gnd>
```

## Dante

The `dante` field type allows you to use the GBV's Dante vocabulary server. All provided vocabularies can be configured. A complete list of available vocabularies can be found at the following address within the `notation` element:

[https://api.dante.gbv.de/voc](https://api.dante.gbv.de/voc)

```xml
<dante ref="DocLanguage">
    <source>languages_gnd</source>
    <field>NORM_LABEL_de, NORM_LABEL_en, NORM_LABEL_fr, NORM_LABEL_es</field>
</dante>
```

## VIAF

The `viaf` field type allows data to be transferred from the VIAF database across all integrated standards databases of different national libraries.

Sample for persons:
```xml
<viaf ref="Author">
    <source>100__a; 400__a; 700_a</source>
    <field>001=NORM_IDENTIFIER; 0247_a=URI; 1001_a=NORM_NAME; 1001_d=NORM_LIFEPERIOD; 1001_q=NORM_SEX; 375__a=NORM_SEX;  700__a=NORM_ALTNAME</field>
</viaf>
```

Sample for places:
```xml
<viaf ref="PlaceOfPublication">
    <!-- # Format: 'mmmiis' -->
    <!-- # mmm - MARC main field -->
    <!-- # ii - indicator 1 + 2 (_ if empty) -->
    <!-- # s - MARC subfield -->
    <source>210__a; 111__a; 100__a; 110__a; 150__a; 151__a;</source>

    <!-- # Format: 'mmmiis=label' -->
    <!-- # mmm - MARC main field -->
    <!-- # ii - indicator 1 + 2 (_ if empty) -->
    <!-- # s - MARC subfield -->
    <!-- # label - label of the field, can be used as message key -->
    <field>001=NORM_IDENTIFIER; 0247_a=URI;</field>
</viaf>
```

## Vocabulary manager - List

The `vocabularyList` field type allows you to transfer data from a specific vocabulary in the vocabulary manager of Goobi workflow. The vocabulary to be used is specified within `source`.

```xml
<vocabularyList ref="singleDigCollection">
    <source>Digital collections</source>
</vocabularyList>
```

If not all values of the vocabulary should be listed, `field` can be used to define a restriction for one or more fields that should contain a certain value:

```xml
<vocabularyList ref="singleDigCollection">
    <source>Digital collections</source>
    <field>public=true;</field>
</vocabularyList>
```

## Vocabulary manager - Dialog selection

If you want the content of a vocabulary from the Goobi vocabulary manager to be accessible via a search box, the type `vocabularySearch` is used. You can use `field` to define which fields of the data records are to be displayed.

```xml
<vocabularySearch ref="SubjectTopic">
    <source>Languages</source>
    <field>Name; Full Name; Description</field>
</vocabularySearch>
```

## People

With the type `person`, a person can be selected. The person can be specified in more details with the elements `<source>` and `<field>`.

```xml
<person ref="Name">
    <source>Source</source>
    <field>Field</field>
</person>
```

## Corporate

With the type `corporate`, a corporate can be selected. The corporate can be specified in more details with the elements `<source>` and `<field>`.

```xml
<corporate ref="Name">
    <source>Source</source>
    <field>Field</field>
</corporate>
```

## Processes

With the type `process`, a process can be selected. The process can be specified in more details with the elements `<source>` and `<field>`.

```xml
<process ref="Title">
    <source>Source</source>
    <field>Field</field>
</process>
```

## Kultur Nav

The type `kulturnav` allows data transfer from the Kulturnav database across all integrated standards databases of different national libraries. The `person` reference and the `<source>` element can be used to retrieve personal data, for example.

```xml
<kulturnav ref="person">
    <source>entityType:Person, entity.dataset:d519f76b-5ce5-4876-906e-7d31a76eb609</source>
</kulturnav>
```

## Database easydb

With the type `easydb`, an easydb database can be specified to import information from.

The element `easydb` defines the desired metadata type, in the attribute `ref` the name of the metadata is configured to which the entry should apply. The element `source` contains the ID of the easydb instance in which the search should be performed. The value must correspond to an instance ID from the file `plugin_metadata_easydb.xml`. In `field` is the ID of the search to be used. The mapping is done using the ID element in the `search` section of the file in `plugin_metadata_easydb.xml`. This allows an individual search query to be configured for each metadata in its own easydb instance. However, the individual search queries can also be reused and entered in `field` for multiple metadata.

```xml
<easydb ref="MetadataName">
    <source>Prize Papers EasyDB</source>
    <field>JourneySearch</field>
</easydb>
```

## Generation of metadata from other values

With the type `generate`, a rule for generating the field can be defined. This allows referencing the content of other metadata or Goobi variables.

The attribute `ref` configures the name of the metadata to which the entry should apply. If the rule should only apply to certain records, an optional XPath expression can be specified in `<condition>` that must be satisfied. Unlike other elements, this field is repeatable and thus allows configurations for a field with different conditions. When generation is executed, all entries are processed from top to bottom, and the first entry for which the condition is met or for which no condition is set is used.

The element `<value>` contains the text to be generated, and arbitrary placeholders in the form of `[NAME]` can be used.

The individual parameters are then defined within the `<item>` elements. Each element contains a `<label>` with the name of the placeholder to be replaced and a `<type>`. The type can either be `xpath` or `variable`. For `xpath`, the value is searched within the current structure element using an XPath expression, while for `variable`, data from the variable replacer of the current process can be used. Using `<regularExpression>` and `<replacement>`, the retrieved value can be further manipulated. If a value is found, the placeholder in the text will be replaced.

```xml
<generate ref="TitleDocMain">
    <condition>goobi:metadata[@name='genre'][text()='Letter']</condition>
    <value>Letter from [ACTOR_FROM] to [ACTOR_TO] at [PLACE], [DATE]</value>

    <item>
        <label>ACTOR_FROM</label>
        <type>xpath</type>
        <field>goobi:metadata[@type='person'][@name='Creator']/goobi:displayName</field>
        <regularExpression>(.+), (.+)</regularExpression>
        <replacement>$2 $1</replacement>
    </item>
    <item>
        <label>ACTOR_TO</label>
        <type>xpath</type>
        <field>goobi:metadata[@type='person'][@name='Receiver']/goobi:displayName</field>
        <regularExpression>(.+), (.+)</regularExpression>
        <replacement>$2 $1</replacement>
    </item>
    <item>
        <label>PLACE</label>
        <type>xpath</type>
        <field>goobi:metadata[@type='group'][@name='location_related_place'][goobi:metadata[@name='location_holdingExternal_relation_type'][text()='is bound from']]/goobi:metadata[@name='location_physicalLocation_related_place']</field>
    </item>
    <item>
        <label>DATE</label>
        <type>variable</type>
        <field>{meta.PublicationYear}</field>
        <regularExpression>([0-9]{4})-[0-9]{2}-[(0-9]{2}</regularExpression>
        <replacement>$1</replacement>
    </item>
</generate>
```