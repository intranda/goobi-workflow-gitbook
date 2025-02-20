# goobi_projects.xml

Die Datei `goobi_projects.xml` konfiguriert die Maske zum Anlegen von Vorgängen. Hier wird projektweise definiert, welche Metadaten und Eigenschaften für bestimmte Publikationstypen erlaubt sind.

Die Datei befindet sich üblicherweise an folgendem Speicherpfad:

```bash
/opt/digiverso/goobi/config/goobi_projects.xml
```

Beispielhaft sieht diese Konfigurationsdatei wie folgt aus:

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

## Definition der Projekte

Für jedes Projekt kann ein `<project>` Element angelegt werden. Der Name des Projektes wird entweder mit dem Parameter `name` oder mit dem Unterelement `<name>` angegeben. Soll eine Konfiguration für Projekte mit verschiedene Namen gelten, können mehrere `<name>` Elemente angegeben werden. Alternativ kann auch ein Regex-Ausdruck statt dem Namen verwendet werden, um mehrere Projekte anzusprechen. Als default Projektkonfiguration sollte immer ein Projekt mit dem Namen `default` eingetragen werden. Wird ein Projekt in Goobi Workflow angelegt, so wird entsprechend der folgenden Reihenfolge nach einer passenden Konfiguration gesucht:

1. Suche nach dem ersten `project` Eintrag, dessen Name dem Projektnamen entspricht oder diesen enthält
2. Suche nach einem `project` Eintrag, dessen Name, interpretiert als regulärer Ausdruck, zum Projektnamen passt
3. Suche nach einem `project` Eintrag mit dem Namen `default`
4. Nutze den ersten `project` Eintrag

## Projektdetails

Die Unterelemente von `<project>` beinhalten eine Reihe Details, die beim Laden der Anlegemaske für Vorgänge in der Benutzeroberfläche berücksichtigt werden.

### Eigenschaften eines neuen Vorgangs

Alle Details, die rund um die Input-Felder wichtig für das Laden der Anlegemaske sind, sind im `<createNewProcess>` Element angegeben. Dieses beinhaltet insbesondere das Element `<itemlist>`, in dem die Input-Felder aufgelistet sind.

#### Liste der Input-Felder

Jedes Input-Feld in der Benutzeroberfläche wird durch ein `<item>` in dieser Liste beschrieben. Mit diesen Einträgen können Textfelder und Dropdown-Menüs hinzugefügt werden. Speziellere Felder, wie zum Beispiel ein Datei-Upload-Bereich, sind weiter unten beschrieben.

Jedes `<item>` Element enthält als Inhalt den Text, der in der Tabelle der Eingabemaske in der Label-Spalte angezeigt wird. Dieser kann zusätzlich durch den Übersetzungsmechanismus von Goobi Workflow mittels der messages Dateien in verschiedene Sprachen übersetzt werden.

Ein `<item>` wird entweder als Textfeld oder als Dropdown-Menü dargestellt. Die folgenden Parameter gelten für beide Arten von Eingabefeldern:

| Attribut | Mögliche Werte | Bedeutung |
| :--- | :--- | :--- |
| `docstruct` | `topstruct`, `firstchild` | Das Attribut `docstruct` kann zwei erlaubte Werte enthalten: `topstruct` und `firstchild`. Diese geben wie bei anderen Konfigurationen an, ob das definierte Metadatum für das oberste Strukturelement oder an das Kind-Element abgelegt werden soll. |
| `from` | `werk`, `vorlage`, `prozess` | Durch das `from` Attribut kann man den Wert als Eigenschaft anlegen lassen. Die erlaubten Werte werk, vorlage und prozess steuern, ob es sich hierbei um eine Vorlageeigenschaft, Werkstückeigenschaft oder Prozesseigenschaft handelt. |
| `isdoctype` | Publikationstyp | Mithilfe des Attributs `isdoctype` lässt sich steuern, für welche Publikationstypen ein Metadatum angezeigt werden soll. Die hier verwendeten Namen der Publikationstypen müssen in der Datei `goobi_opac.xml` definiert worden sein. |
| `isnotdoctype` | Publikationstyp | Mithilfe des Attributs `isnotdoctype` lässt sich steuern, für welche Publikationstypen ein Metadatum nicht angezeigt werden soll. Dieses Attribut kann verendet werden, wenn ein Eingabefeld zu allen außer einem bestimmten Dokumenttypen passt. Die hier verwendeten Namen der Publikationstypen müssen in der Datei `goobi_opac.xml` definiert worden sein. |
| `required` | `true`, `false` | Wird `required` auf `true` gesetzt, dann ist das Eigabefeld in der Benutzeroberfläche als verpflichtend markiert. Wird ein solches Feld beim Ausfüllen des Formulars freigelassen, weist Goobi den Nutzer darauf hin und der Erstellvorgang ist nicht beendbar. |
| `initStart` | Text | Durch `initStart` lässt sich ein statischer Präfix hinzufügen. Außerdem kann der enthaltene Wert automatisch erzeugt werden. Diese Einstellung macht insbesondere für Identifier Sinn. |
| `initEnd` | Text | Durch `initEnd` lässt sich ein statischer Suffix hinzufügen. Außerdem kann der enthaltene Wert automatisch erzeugt werden. Diese Einstellung macht insbesondere für Identifier Sinn. |
| `ughbinding` | `true`, `false` | Bei der Angabe von `ughbinding="true"` wird der Wert der Eigenschaft oder des Metadatums durch das Ergebnis der OPAC Abfrage gefüllt. |
| `metadata` | `MetadataType` | Wird das Attribut `metadata` angegeben, wird hier nicht nur eine Eigenschaft definiert, sondern auch ein Metadatum des angegebenen Typs in der zugehörigen METS-Datei. Der hier angegebene Wert muss mit einer Metadatendefinition im verwendeten Regelsatz übereinstimmen. |
| `autogenerated` | `true`, `false` | Mit diesem Parameter kann festgelegt werden, ob das Feld automatisch mit einem Identifier gefüllt werden soll, sofern es keinen Inhalt hat. |

##### Dropdown-Menüs

Sobald ein `<item>` den Parameter `multiselect` und Unterelemente `<select>` enthält, wird es nicht mehr als Textfeld dargestellt, sondern als Dropdown-Menü. Der `multiselect`-Parameter kann auf `true` oder `false` gesetzt werden, um die Auswahl mehrerer Einträge zu erlauben oder zu verbieten.

Jedes `<select>` Element kann einen `label` Parameter haben. Der `label`-Text wird im Menü angezeigt, während der Inhalt des `<select>` Elements technisch weiterverarbeitet wird. Damit kann für die Anzeige ein besser lesbarer Alternativname angegeben werden.

Auch ein `<item>`, das als Dropdown-Menü dargestellt wird, benötigt ein Label. Dieses wird parallel zu den `<select>` Elementen angegeben.

Soll zum Beispiel ein Städtekürzel beim Erstellen eines Vorgangs auswählbar sein, wäre es für Anwender sinnvoll, die ausgeschriebenen Namen im Menü angezeigt zu bekommen:

```xml
<item multiselect="false" required="true">
    Physical location
    <select label="Berlin">B</select>
    <select label="Göttingen">GOE</select>                    
    <select label="Hannover">H</select>                    
</item>
```

##### Ausblenden von Input-Feldern

Mit dem `<hide>` Element können Input-Felder, also hier definierte `<item>` Elemente ausgeblendet werden. Das Feld kann zum Beispiel folgende Werte beinhalten: `collections`, `doctype`, `preferences`, `images` und `processtitle`. 

Mittels `collections` kann die Auswahl der Sammlung ausgeblendet werden, `doctype` steuert die Anzeige des Feldes zur Auswahl des Dokumententyps, `preferences` das Auswahlfeld für den Regelsatz, `images`die Eingabe für die  erwartete Zahl an Digitalisaten und `processtitle` die Anzeige des generierten Vorgangstitels.

##### Vorgangstitel

Soll der Vorgangstitel automatisch generiert werden, so können mit dem Element `<processTitle>` Bildungsvorschriften für die Titel angegeben werden. Vorgangstitel können für bestimmte Dokumententypen unterschiedlich generiert werden. Um einen Dokumenttyp einer Bildungsvorschrift zuzuordnen, wird der Parameter `isdoctype` verwendet. Alternativ können alle Dokumenttypen verwendet und nur ein bestimmter Typ mit dem Parameter `isnotdoctype` ausgeschlossen werden.

Zwischen Anfangs- und Endelement von `<processTitle>` steht ein Ausdruck, der den zu generierenden Titel beschreibt. Textpassagen werden in einfachen Anführungszeichen geschrieben und als Variablennamen können alle weiter oben definierten Eigenschaften verwendet werden. Alle Elemente werden mit dem `+` Operator verkettet.

Um zum Beispiel für alle Dokumente, die kein `periodical` sind, einen Titel zu generieren, der den Autor und den Titel des Dokumentes beinhaltet, wäre folgender Eintrag sinnvoll:

```xml
<processTitle isnotdoctype"periodical">Author + '_' + Title</processTitle>
```

Mit dem `replacewith` Parameter kann bei Bedarf eine Zeichenkette angegeben werden, mit der alle ungültigen Buchstaben und Sonderzeichen im automatisch generierten Vorgangstitel ersetzt werden sollen. Ist die Zeichenkette `""`, so werden alle ungültigen Zeichen entfernt. Auch wenn dieser Parameter fehlt, werden alle Sonderzeichen ersatzlos entfernt.

#### Auswahl des OPAC-Katalogs

Die OPAC-Katalog-Abfrage kann aktiviert werden, indem innerhalb des Parameters `<opac>` das Attribut `use` auf den Wert `true` gesetzt wird. Der vorausgewählte Katalog kann dabei im Unterlement `<catalogue>` definiert werden. Wenn der Wert nicht gesetzt wurde oder keinem Eintrag aus der Datei `goobi_opac.xml` entspricht, wird der erste dort definierte Katalog als Standardwert genutzt.

#### Verwenden anderer Vorgänge als Vorlagen

Um die Metadaten aus bereits vorhandenen Vorgängen zu importieren, muss im Element `<templates>` das Attribut `use` auf den Wert `true` gesetzt werden. Dadurch steht die Option `Auswählen aus vorhandenen Vorgängen` zur Verfügung, in der alle Vorgänge aufgelistet sind, bei denen die Checkbox `In Auswahlliste anzeigen` während des Anlegens aktiviert wurde.

#### Standard Dokumenttyp

Der beim Öffnen der Anlegemaske ausgewählte Publikationstyp kann im Feld `<defaultdoctype>` festgelegt werden. Die hier genutzte Bezeichnung stammt aus der `doctypes` Definition der Konfigurationsdatei `goobi_opac.xml`.

#### Generierung von Metadaten

Durch die Verwendung des `<metadatageneration />` Elements mit dem Parameter `use="true"` können beim Anlegen eines Vorgangs automatisch weitere Metadaten generiert werden.

#### Hochladen von Dateien

Mit der Konfiguration von `<fileupload>` kann der Upload-Bereich freigeschaltet werden. Damit lassen sich zum neu erzeugten Vorgang bereits Dateien hochladen. Welche Ordner zur Auswahl stehen, kann im Unterfeld `<folder>` konfiguriert werden.

Mit dem `regex`-Parameter kann angegeben werden, welche Dateinamen in der Benutzeroberfläche vom Hochladen-Button akzeptiert werden. Entspricht die vom Benutzer ausgewählte Datei nicht dem Regex-Ausdruck, so wird die Datei nicht hochgeladen und eine Fehlermeldung angezeigt. Wird der Regex-Parameter weggelassen oder eine leere Zeichenkette angegeben, so sind Dateien aller Dateitypen und -namen hochladbar. Da der Regex-Ausdruck von Primefaces ausgewertet wird, muss er in Slashes eingefasst sein:

Gültige Schreibweise:

`/^.*\.pdf$/`

Ungültige Schreibweise:

`^.*\.pdf$`

Der `messageKey`-Parameter gibt einen Key an, der in `messages_xx.properties`-Dateien dazu verwendet werden kann, individuelle Fehlermeldungen zu hinterlegen. Wird zum Beispiel wie oben gezeigt ein Dateiupload auf PDF-Dateien beschränkt, dann kann in den messages-Dateien in allen Sprachen unter dem hier angegebenen Key eine Fehlermeldung angegeben werden, die auf einen falschen Dateityp hinweist. Wird der Parameter weggelassen oder der Key nicht gefunden, so wird eine Standard-Fehlermeldung angezeigt.

### Tiff-Header

Im `<tifheader>` Element können Werte angegeben werden, die in die Tiffheader geschrieben werden sollen. Hier kann für jeden Publikationstyp, der zuvor in einem `<item>` definiert wurde, ein eigener Text definiert werden.

Ist zum Beispiel ein `<item>monograph</item>` definiert worden, so kann hier beispielweise folgendes eingetragen werden:

```xml
<monograph>'|DOC_TYPE'+$Doctype+'|HAUPTTITEL'+Titel+'|AUTOREN/HERAUSGEBER'+Autoren+'JAHR'+Erscheinungsjahr+'|ERSCHEINUNGSORT'+Erscheinungsort+'|'</monograph>
```

### Import aus DMS

Um Daten aus einem Dokumenten-Management-System zu importieren, kann das Element `<dmsImport>` angegeben werden.

### Validierung

Daten des Formulars können validiert werden. Validierungen können im Element `<validate>` spezifiziert werden.