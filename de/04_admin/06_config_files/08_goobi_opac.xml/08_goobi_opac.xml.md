# goobi_opac.xml

In der Konfigurationsdatei `goobi_opac.xml` wird die Kommunikation von Goobi workflow mit externen Datenquellen festgelegt. Dies betrifft zumeist Systeme wie Bibliothekskataloge. Die Datei befindet sich üblicherweise an folgendem Speicherpfad:

```bash
/opt/digiverso/goobi/config/goobi_opac.xml
```

Beispielhaft sieht diese Konfigurationsdatei wie folgt aus:

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

## Publikationstypen

In dem Element `<doctypes>` können mehrere Publikationstypen definiert werden. Jeder Typ steht in einem eigenen `<type>`-Element und hat einige Eigenschaften, die über Parameter und Unterelemente angegeben werden.

### Eigenschaften eines Publikationstyps

Alle wichtigen Eigenschaften eines Publikationstyps werden als Parameter im `<type>`-Element angegeben. Folgende Parameter können verwendet werden:

| Attribut | Mögliche Werte | Bedeutung |
| :--- | :--- | :--- |
| `title` | Text | Dieses Feld gibt den Titel des Publikationstypen an. Der Titel ist ein technisch einfach nutzbarer Name, der mit dem `<label>`-Unterelement übersetzt werden kann. |
| `isContainedWork` | `true`, `false` | Dieser Wert kann auf `true` gesetzt werden, wenn es sich bei diesem Publikationstyp um einen Teil eines anderen Publikationstyps handelt. Dies kann beispielsweise verwendet werden, wenn in einem Buch herausnehmbare Landkarten enthalten sind und dieser Publikationstyp die beliliegenen Landkarten darstellt. **Hinweis:** Dieser Parameter ist weitgehend veraltet und sollte nicht mehr verwendet werden. |
| `isMultiVolume` | `true`, `false` | Dieser Wert kann auf `true` gesetzt werden, wenn es sich bei dem Publikationstyp um eine mehrbändige Ausgabe handelt, zum Beispiel ein einzelner Band eines Lexikons. |
| `isPeriodical` | `true`, `false` | Dieser Wert kann auf `true` gesetzt werden, wenn es sich bei dem Publikationstyp um eine regelmäßige Ausgabe, zum Beispiel eine Zeitung, handelt. |
| `rulesetType` | Name aus `ruleset.xml` | Mit diesem Feld kann ein Regelsatz angegeben werden, der mit diesem Publikationstyp verknüpft werden soll. |
| `rulesetChildType` | Name aus `ruleset.xml` | Mit diesem Feld kann ein Regelsatz-Unterelement angegeben werden, das mit diesem Publikationstyp verknüpft werden soll. |
| `tifHeaderType` | Text | Mit diesem Feld kann eine Bezeichnung angegeben werden, die beim Export zu Tiff-Dateien in den Dateiheader geschrieben werden soll. |

### Übersetzung des Titels

Die im `title`-Parameter angegebene Bezeichnung eines Publikationstyps wird softwareintern verwendet und ist daher für Anwender nicht immer gut lesbar und wird nicht automatisch übersetzt. Daher kann der Name des Publikationstyps mit dem `<label>`-Element in verschiedene Sprachen übersetzt werden. Mit dem `language`-Parameter wird das Sprach-Kürzel angegeben. Je nach Konfiguration werden üblicherweise folgende Sprachen unterstützt:

```xml
<type title="periodical">
    <label language="de">Deutsche Übersetzung</label>
    <label language="en">Englische Übersetzung</label>
    <label language="es">Spanische Übersetzung</label>
    <label language="fr">Französische Übersetzung</label>
    <label language="it">Italienische Übersetzung</label>
    <label language="iw">Hebräische Übersetzung</label>
    <label language="nl">Niederländische Übersetzung</label>
    <label language="pt">Portugiesische Übersetzung</label>
</type>
```

### Mapping zu anderen Datenformaten

Es kann vorkommen, dass ein Publikationstyp mit einer Suchfunktion oder mit externen Datenformaten über bestimmte Bezeichnungen oder Kürzel gefunden werden können soll, die nicht aus dem Titel ableitbar sind. Dazu können für jeden Typen mit dem Unterelement `<mapping>id42</mapping>` weitere Bezeichnungen angegeben werden. Wird dann zum Beispiel nach der ID `id42` gesucht, so wird der entsprechende Publikationstyp gefunden.

## Kataloge

Goobi kann Metadaten aus verschiedenen Katalogen verwenden. Diese werden mit dem `<catalogue>` Element direkt im `<opacCatalogues>` Element eingetragen. Für jedes Katalog-Element wird mit dem `title` Parameter der offizielle Name des jeweiligen Katalogs angegeben.

### Konfiguration eines Katalogs

Einige weitere Eigenschaften eines Katalogs werden im Unterelement `<config>` als Parameter angegeben. Folgende Parameter können verwendet werden:

| Attribut | Mögliche Werte | Bedeutung |
| :--- | :--- | :--- |
| `opacType` | OPAC-Typ | Mit diesem Parameter kann der OPAC-Typ der vom Katalog verwendeten Datenbank angegeben werden. Dies kann zum Beispiel `PICA`, `ALMA-MARC` oder `GBV-MARC` sein. |
| `description` | Text | Hier kann eine Beschreibung des Katalogs angegeben werden. |
| `protocol` | Protokoll | Dieser Parameter wird üblicherweise auf `http://` oder `https://` gesetzt, sofern das Protokoll nicht bereits im `address` Parameter enthalten ist. |
| `address` | URL | Dieser Parameter gibt den Domain-Namen oder die IP-Adresse der API des Katalog-Services an. Wird hier das Netzwerkprotokoll angegeben, so muss der `protocol` Parameter leer bleiben. |
| `port` | Portnummer | Mit der Portnummer kann ein besonderer Netzwerkport der API des Katalog-Services angegeben werden. Üblicherweise ist dies der Standard-HTTP-Port `80`. |
| `database` | Zahl | Mit diesem Parameter kann die Datenbank-Version angegeben werden, die bei API-Anfragen verwendet werden soll. |
| `charset` | Zeichensatz | Mit diesem Parameter kann ein Zeichensatz angegeben werden, mit dem die Datenbank die Datensätze zurückgeben soll. |
| `iktlist` | Dateipfad | Dieser Parameter wird nur verwendet, wenn der Katalog eine PICA-Datenbank verwendet. Der Dateiname muss auf eine IKTLIST-Datei verweisen, die Informationen über Mediennummernsysteme bereitstellt. |
| `ucnf` | Text | Dieser Parameter wird verwendet, um UCNF-Informationen in die URL der API-Anfrage einzufügen. |

### Optionen für die Suche

Metadaten werden in Katalogen mithilfe bestimmter Nummern identifiziert (zum Beispiel ISBN oder ISSN). Sollen in Goobi Metadaten anhand einer vorgegebenen Nummer aus dem jeweiligen Katalog importiert werden, können mit dem `<searchFields> Element verschiedene Nummernsysteme aufgelistet werden. Ein Anwender kann dann im folgenden Beispiel eine ISBN-Nummer eingeben und dazu passend das ISBN-Feld auswählen:

```xml
<searchFields>
    <searchField label="LCCN" value="12" />
    <searchField label="ISBN" value="7" />
    <searchField label="ISSN" value="8" />
</searchFields>
```

Dabei stellt jedes `<searchField>` Element eine Option in dem zugehörgigen Dropdown-Menü dar. Der in `label` angegebene Text wird auf der Nutzeroberfläche dargestellt. Der in `value` definierte Wert ist die interne ID des Nummernsystems. Je nach Katalog kann auch eine textbasierte ID verwendet werden. Das kann zum Beispiel so aussehen:

```xml
<searchField label="ISBN" value="alma.isbn"/>
<searchField label="ISSN" value="alma.issn"/>
```

Detailierte Informationen über unterstützte Nummernsysteme können von der jeweiligen Katalog-API abgefragt werden. Dies ist eine XML-Datei, die direkt im Browser aufgerufen werden kann. Die Domain muss entsprechend dem verwendeten Anbieter angepasst werden.

```xml
https://opac.intranda.com/XML=1.0/IKTLIST
https://kxp.k10plus.de/XML=1.0/IKTLIST
```

### Mapping zu Publikationstypen

Wie oben beschrieben, können Publikationstypen mit alternativen Bezeichnungen gefunden werden. Zusätzlich ist es in `<catalogue>` Elementen möglich, mit dem `<specialmapping>` Element katalogspezifische Bezeichnungen (und damit auch Kataloge) zu Publikationstypen zu verknüpfen. Damit können über die alternativen Bezeichnungen eines Katalogs passende Publikationstypen definiert und gefunden werden.

Dabei verweist der `type`-Parameter des `<specialmapping>`-Elements auf den `title` des zuvor definierten Publikationstypen. Das `<specialmapping>` Element beinhaltet eine alternative Bezeichnung. Folgendes Beispiel würde für einen K10Plus-Katalog den Suchbegriff `k10plus_periodical` mit dem Publikationstyp `periodical` verknüpfen:

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

### Anpassen von Datensätzen aus MARC-Dateien

Werden Datensätze aus Katalogen abgefragt, so werden diese unter anderem über MARC-Dateien in Goobi importiert. Datensätze aus diesen Dateien können durch bestimmte Ersetzungsmuster angepasst werden. Dazu wird das `<beautify>` Element als direktes Unterelement des entsprechenden `<catalogue>` Elements verwendet und kann beliebig viele `<setvalue>` Befehle enthalten.

Da die Bearbeitung der MARC-Daten mit diesen Befehlen sehr komplex werden kann, werden hier auf Basis des folgenden MARC-Daten-Ausschnitts nur ein paar einfache Beispiele beschrieben.

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

Mit dem folgendem Befehl können bestimmte Werte ersetzt werden. Stellt sich zum Beispiel heraus, dass manche Datensätze vom Typ `book` eine ungültige Jahreszahl (`year`) haben, können falsche Daten korrigiert werden. Der `setvalue`-Befehl bestimmt, dass in jedem mit der inneren `<condition>` angesprochenen `datafield` mit Tag `book` das `subfield` mit dem Parameter `code="year"` den Wert `1900` bekommen soll. Die `<condition>` besagt, dass alle `datafield` Elemente berücksichtigt werden sollen, die das Tag `book` haben und bei denen ein Unterelement mit `code="year"` und dem Wert `190` vorhanden ist.

```xml
<beautify>
    <setvalue tag="book" subtag="year" value="1900">
        <condition tag="book" subtag="year" value="190" />
    </setvalue>
</beautify>
```

Daten können mit dem `<setvalue>`-Befehl gefiltert werden. Möchte man zum Beispiel die `other_id` Elemente entfernen, kann deren Wert mit einer leeren Zeichenkette überschrieben werden.

**Hinweis:** Ein Sternchen (*) ist ein Platzhalter für ein beliebigen Wert. Reguläre Ausdrücke werden nicht unterstützt.

```xml
<beautify>
    <setvalue tag="*" subtag="other_id" value="">
        <condition tag="*" subtag="other_id" value="*" />
    </setvalue>
</beautify>
```

Datensätze können auch um neue Eigenschaften ergänzt werden. Dies funktioniert allerdings nur bedingt, weil nur auf die Daten aus der MARC-Datei und aus dem `<setvalue>` Befehl zurückgeriffen werden kann. So ist es zum Beispiel möglich, Datensätze mit bestimmten Inhalten neue Tags zu vergeben:

```xml
<beautify>
    <setvalue tag="paper" subtag="target_group" value="students">
        <condition tag="paper" subtag="author" value="Dr. Arthur Williams" />
    </setvalue>
</beautify>
```

{% hint style="info" %}
**Hinweis:**\
Bitte beachten Sie, dass Goobi ursprünglich auf die Kommunikation mit PICA-Katalogen ausgerichtet war. Mittlerweile werden auch viele weitere verschiedene Katalogsysteme unterstützt. Diese bedingen jedoch oftmals eine sehr individuelle Konfiguration z.B. für die Kommunikation über das Protokoll Z39.50 oder unter Nutzung von SRU.
{% endhint %}