# goobi_metadataDisplayRules.xml

In der Konfigurationsdatei `goobi_metadataDisplayRules.xml` wird festgelegt, wie die Metadaten innerhalb des Metadateneditors von Goobi angezeigt werden sollen. Sie befindet sich üblicherweise an folgendem Pfad im Dateisystem.

```bash
/opt/digiverso/goobi/config/goobi_metadataDisplayRules.xml
```

In dieser Konfigurationsdatei wird beschrieben, wie einzelne Metadatenfelder dargestellt werden sollen. So kann unter anderem festgelegt werden, das Felder beispielsweise als Eingabefelder, Auswahllisten, Read-Only-Felder etc. angezeigt werden und entsprechend unterschiedlich durch den Nutzer bearbeitet werden können. Beispielhaft hier einmal eine solche Konfigurationsdatei:

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

In dieser Konfigurationsdatei kann innerhalb des Attributs `projectName` festgelegt werden, für welche Projekte diese individuell konfigurierte Anzeige gelten soll.

Die mit `ref` angegebenen IDs verweisen auf die Metadaten-Namen, die in der Datenbank zu dem entsprechenden Projekt (bzw. Vorgang) existieren.

Die meisten Elemente haben ein Unterelement `label`. Dieses kann einen Text beinhalten, der das Input-Feld beschreibt. Üblicherweise ist das der Name des entsprechenden Metadatums, er kann jedoch zur besseren Lesbarkeit auch davon abweichen.

Darüber hinaus kann aus einer Liste verschiedener Feldtypen ausgewählt werden:
<!--- Diese Liste basiert auf dem Enum org.goobi.api.display.enums.DisplayType -->

## Input Box

Der Typ `input` wird als normales einzeiliges Eingabefeld dargestellt.

```xml
<input ref="PlaceOfPublication">
    <label>Göttingen</label>
</input>
```

## Text Area

Der Typ `textarea` ist ähnlich zur Input Box. Eine Text-Area ist jedoch mehrzeilig und erlaubt eine Anpassung der Anzeigegröße des Feldes.

```xml
<textarea ref="TitleDocMain">
    <label />
</textarea>
```

## Read only Field

Der Typ `readonly` ist ähnlich zur Input Box, allerdings erlaubt dieses keine Änderung des Feldinhalts.

```xml
<readonly ref="CatalogIDDigital">
    <label />
</readonly>
```

## Select Box

Die Select Box `select1` erlaubt die Auswahl **eines** Wertes aus einer Liste von Werten. Hierbei wird zwischen dem angezeigten Wert (`label`) und dem tatsächlich intern zu speichernden Wert (`value`) unterschieden. Mit dem `selected` Parameter kann **ein** `<item>` Element vorausgewählt werden.

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

Die Multi Select Box `select` erlaubt die Auswahl **mehrerer** Werte, die alle innerhalb des Metadatenfeldes gespeichert werden sollen. Auch hier wird zwischen dem anzeigten Wert (`label`) und dem intern gespeicherten Wert (`value`) unterschieden. Mit dem `selected` Parameter können **mehrere** `<item>` Elemente vorausgewählt werden.

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

Der Feldtyp `htmlInput` erlaubt die Eingabe von Texten mit optischen Formatierungsmöglichkeiten. So lässt sich beispielsweise Text fett oder kursiv auszeichnen und wird samt den Formatierungen in der METS-Datei gespeichert.

```xml
<htmlInput ref="Description">
    <label></label>
</htmlInput>
```

## GeoNames

Der Typ `geonames` erlaubt die Suche und Auswahl von Orten innerhalb der GeoNames-Datenbank.

```xml
<!-- Geonames as selectable field, in ruleset the PlaceOfPublication has to have this attribute then: normdata="true" -->
<geonames ref="PlaceOfPublication">
    <label></label>
</geonames>
```

## GND

Der Feldtyp `gnd` erlaubt die Suche und Datenübernahme von Einträgen aus der Gemeinsamen Normdatenbank der Deutschen Nationalbibliothek.

```xml
<gnd ref="Subject">
    <label />
</gnd>
```

## Dante

Der Feldtyp `dante` erlaubt die Nutzung des Dante-Vokabularservers des GBV. Hierbei können sämtliche zur Verfügung gestellten Vokabulare konfiguriert werden. Eine vollständige Liste der zur Verfügung stehenden Vokabulare findet sich unter der folgenden Adresse innerhalb des `notation` Elements:

[https://api.dante.gbv.de/voc](https://api.dante.gbv.de/voc)

```xml
<dante ref="DocLanguage">
    <source>languages_gnd</source>
    <field>NORM_LABEL_de, NORM_LABEL_en, NORM_LABEL_fr, NORM_LABEL_es</field>
</dante>
```

## VIAF

Der Feldtyp `viaf` erlaubt die Datenübernahme aus der VIAF-Datenbank über alle integrierten Normdatenbanken verschiedener Nationalbibliotheken hinweg.

Beispiel für Personen
```xml
<viaf ref="Author">
    <source>100__a; 400__a; 700_a</source>
    <field>001=NORM_IDENTIFIER; 0247_a=URI; 1001_a=NORM_NAME; 1001_d=NORM_LIFEPERIOD; 1001_q=NORM_SEX; 375__a=NORM_SEX;  700__a=NORM_ALTNAME</field>
</viaf>
```

Beispiel für Orte:
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

## Vokabularmanager - Liste

Der Feldtyp `vocabularyList` erlaubt die Datenübernahme aus einem konkreten Vokabular des Vokabularmanagers von Goobi workflow. Innerhalb von `source` ist hierbei das zu verwendende Vokabular genannt.

```xml
<vocabularyList ref="singleDigCollection">
    <source>Digital collections</source>
</vocabularyList>
```

Sollen nicht alle Werte des Vokabulars aufgeführt werden, so kann mittels `field` eine Einschränkung für eines oder mehrere Felder definiert werden, die einen bestimmten Wert enthalten sollen:

```xml
<vocabularyList ref="singleDigCollection">
    <source>Digital collections</source>
    <field>public=true;</field>
</vocabularyList>
```

## Vokabularmanager - Dialogauswahl

Soll der Inhalt eines Vokabulars aus dem Goobi Vokabularmanager über eine Suchbox möglich sein, wird der Typ `vocabularySearch` verwendet. Hierbei kann mittels `field` definiert werden, welche Felder der Datensätze angezeigt werden sollen.

```xml
<vocabularySearch ref="SubjectTopic">
    <source>Languages</source>
    <field>Name; Full Name; Description</field>
</vocabularySearch>
```

## Personen

Mit dem Typ `person` kann eine Person ausgewählt werden. Die Person kann mit den Elementen `source>` und `<field>` näher spezifiziert werden.

```xml
<person ref="Name">
    <source>Source</source>
    <field>Field</field>
</person>
```

## Unternehmen

Mit dem Typ `corporate` kann ein Unternehmen ausgewählt werden. Das Unternehmen kann mit den Elementen `source>` und `<field>` näher spezifiziert werden.

```xml
<corporate ref="Name">
    <source>Source</source>
    <field>Field</field>
</corporate>
```

## Vorgänge

Mit dem Typ `process` kann ein Vorgang ausgewählt werden. Der Vorgang kann mit den Elementen `source>` und `<field>` näher spezifiziert werden.

```xml
<process ref="Title">
    <source>Source</source>
    <field>Field</field>
</process>
```

## Kultur Nav

Der Typ `kulturnav` erlaubt die Datenübernahme aus der Kulturnav-Datenbank über alle integrierten Normdatenbanken verschiedener Nationalbibliotheken hinweg. Mit der Referenz `person` und dem `<source>` Element können zum Beispiel Personendaten abgefragt werden.

```xml
<kulturnav ref="person">
    <source>entityType:Person, entity.dataset:d519f76b-5ce5-4876-906e-7d31a76eb609</source>
</kulturnav>
```

## Datenbank easydb

Mit dem Typ `easydb` kann eine easydb Datenbank für das Importieren von Informationen angegeben werden.

Das Element `easydb` definiert den gewünschten Metadatentyp, im Attribut `ref` wird der Name des Metadatums konfiguriert, auf den der Eintrag zutreffen soll. Das Element `source` enthält die ID der easydb Instanz, in der die Suche erfolgen soll. Der Wert muss einer instance ID aus der Datei `plugin_metadata_easydb.xml` entsprechen. In `field` steht die ID der zu nutzenden Suche. Die Zuordnung erfolgt über das Element ID im `search` Bereich der Datei in `plugin_metadata_easydb.xml`. Damit kann für jedes Metadatum eine individuelle Suchanfrage in einer eigenen easydb Instanz konfiguriert werden. Die einzelnen Suchanfragen lassen sich jedoch auch nachnutzen und können bei mehreren Metadaten in `field` eingetragen werden.

```xml
<easydb ref="MetadataName">
    <source>Prize Papers EasyDB</source>
    <field>JourneySearch</field>
</easydb>
```

## Generierung von Metadaten aus anderen Werten

Mit dem Typ `generate` kann eine Regel zur Generierung des Feldes definiert werden. Dabei kann auf den Inhalt anderer Metadaten oder Goobi-Variablen zurückgegriffen werden.
Im Attribut `ref` wird der Name des Metadatums konfiguriert, auf den der Eintrag zutreffen soll. Wenn die Regel nur für bestimmte Datensätze gelten soll, kann optional in `<condition>` ein XPath Ausdruck angegeben werden, der erfüllt werden muss. Im Gegensatz zu den anderen Elementen ist dieses Feld wiederholbar und erlaubt daher Konfigurationen für ein Feld mit unterschiedlichen Bedingungen. Wenn die Generierung ausgeführt wird, werden alle Einträge von oben nach unten abgearbeitet und der erste Eintrag genutzt, bei dem die Bedinung erfüllt ist oder bei dem keine Bedinung festgelegt wurde.

Das Element `<value>` enthält den zu bildenden Text. Dabei können beliebige Platzhalter in Form von `[NAME]` verwendet werden.

Die einzelnen Parameter werden dann innerhalb der `<item>` Elemente definiert. Jedes Element enthält ein `<label>` mit dem Namen des zu ersetzenden Platzhalters und einen `<type>`. Der kann entweder `xpath` oder `variable` sein. Bei `xpath` wird der zu suchende Wert mittels XPAth Ausdruck innerhalb des aktuellen Strukturelements gesucht, bei `variable` kann auf die Daten des VariablenReplacers des aktuellen Vorgangs zurückgegriffen werden. Mittels `<regularExpression>` und `<replacement>` lässt sich der ermittelte Wert noch manipulieren. Wenn ein Wert gefunden wurde, wird der Platzhalter im Text ersetzt.

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