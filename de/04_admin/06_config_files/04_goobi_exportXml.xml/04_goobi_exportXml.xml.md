# goobi_exportXml.xml

In der Datei `goobi_exportXml.xml` werden technische Details zu den verwendeten Eigenschaften und zugehörigen XML-Namensräumen beim Generieren von Laufzettel-Dateien angegeben.

Die Datei befindet sich üblicherweise an folgendem Speicherpfad:

```bash
/opt/digiverso/goobi/config/goobi_exportXml.xml
```

Beispielhaft sieht diese Konfigurationsdatei wie folgt aus:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<config_exportXml>

	<namespace name="mets" value="http://www.loc.gov/METS/" />
	<namespace name="mods" value="http://www.loc.gov/mods/v3" />
	<namespace name="goobi" value="http://meta.goobi.org/v1.5.1/" />
	<namespace name="xlink" value="http://www.w3.org/1999/xlink" />
	<namespace name="dv" value="http://dfg-viewer.de/" />
	<namespace name="wt" value="http://wellcome.ac.uk/" />

	<mets>
		<property name="shelfmarksource" value="//mets:mets/mets:dmdSec[1]/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi/goobi:metadata[@name='shelfmarksource']" />
		<property name="TitleDocMain" value="//mets:mets/mets:dmdSec[1]/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi/goobi:metadata[@name='TitleDocMain']" />
		<property name="CorporateName" value="//mets:mets/mets:dmdSec[1]/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi/goobi:metadata[@name='CorporateName']" />
		<property name="PublicationYear" value="//mets:mets/mets:dmdSec[1]/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi/goobi:metadata[@name='PublicationYear']" />
	</mets>

	<!--
	<anchor>
		<property name="ManifestationType" value="//mets:mets/mets:dmdSec[1]/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi/goobi:metadata[@name='_ManifestationType']" />
	</anchor>
	-->

</config_exportXml>
```

## Allgemeines

Diese Konfigurationsdatei wird dafür verwendet, weitere Eigenschaften anzugeben, die beim Export von Laufzettel-Dateien berücksichtigt werden sollen. Da diese Eigenschaften aus verschiedenen Bereichen zusammengetragen werden können, muss für jede Eigenschaft angegeben werden, wo sie definiert ist. Dies geschieht mit Hilfe von Namensräumen, die vorher ebenfalls definiert werden.

## Definieren von Namensräumen

Mit den `<namespace>` Elementen werden Namensräume definiert, mit denen weitere Eigenschaften für den Export von Metadaten verwendet werden können. Es gibt einige Projekte und Institutionen, die solche Namensräume definieren. In dieser Konfigurationsdatei wird für jede benötigte Namensraumdefinition ein `<namespace>` Element angelegt.

Namensräume werden durch einen Namen oder eine Abkürzung identifiziert, der mit dem `name` Parameter angegeben wird. Dieser sollte kurz und aussagekräftig sein, da er später oft verwendet wird. Namensraum-Namen dürfen nicht mehrfach vorkommen. Üblicherweise wird der Projektname oder eine Abkürzung davon verwendet. Der Projektname ist in der Regel aus der Domain in der angegeben URL ersichtlich.

Dementsprechend verweisen Namensräume auf eine URL, die im Parameter `value` definiert wird. Diese URL muss auf eine XML-Spezifikation verweisen, die weitere Informationen über den jeweiligen Namensraum und die verfügbaren Eigenschaftsnamen beinhaltet. Weitere Informationen gibt es in den jeweiligen Dokumentationen zu den Namensraum-Spezifikationen.

Wird zum Beispiel folgender Namensraum definiert,

```xml
<namespace name="mets" value="http://www.loc.gov/METS/" />
```

so kann später ein Element `mets:xmlData` verwendet werden. Goobi kann dann zuordnen, dass im Namensraum `mets`, der wiederum in der Spezifikation unter `http://www.loc.gov/METS/` definiert ist, nach dem Element `xmlData` gesucht werden soll. Dort ist es dem Projekt entsprechend definiert.

## Definieren von Eigenschaften

Eigenschaften, die beim Export berücksichtigt werden sollen, werden in `<property>` Elementen angegeben. Der Titel, der im `name` Parameter angegeben wird, wird für die Struktur des exportierten Laufzetteldokumentes weiterverwendet. Der `value` Parameter beinhaltet ein oder mehrere Eigenschaften, die wie folgt aufgebaut sind.

### Syntax für Eigenschaften

Alle Eigenschaften werden mit Schrägstrichen (`/`) getrennt. Zusätzlich beginnt der gesamte Eintrag mit zwei Schrägstrichen. Die grundlegende Syntax ist wie folgt:

```xml
value="//field1/field2/field3"
```

Da in der Liste von Namensräumen kein Standardnamensraum definiert werden kann, wird jede Eigenschaft mit einem Namensraum versehen und es ergibt sich folgende Syntax:

```xml
value="//namespace1:field1/namespace2:field2/namespace3:field3"
```

Es können beliebig viele Elemente angegeben werden. Es können nur Namensräume verwendet werden, die zuvor in den `<namespace>` Elementen definiert worden sind. Entsprechend der Namensräume können nur bestimmte Eigenschaften angegeben werden. Das sieht zum Beispiel so aus:

```xml
value="//mets:mets/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi"
```

Es kann vorkommen, dass Eigenschaften als Listen vorliegen. In diesem Fall wird mit eckigen Klammern die Nummer des Listenelements angegeben. Zu beachten ist, dass die Zählung bei 0 beginnt. Im folgenden Beispiel wird das zweite Element aus der Liste `dmdSec` verwendet. (Das erste Element hätte dann die Nummer 0.)

```xml
mets:dmdSec[1]
```

Außerdem ist es möglich, bei komplexeren Eigenschaften zu selektieren, welcher Bestandteil der Eigenschaft verwendet werden soll. Im folgenden Beispiel wird aus dem Element `metadata` das Unterelement mit der Eigenschaft `name` = `PublicationYear` ausgewählt.

```xml
goobi:metadata[@name='PublicationYear']
```

### meta.xml oder meta_chanor.xml

Wird nur eine `meta.xml` verwendet, um den Vorgang zu beschreiben, so werden alle `<property>` Elemente innerhalb eines `<mets>` Elementes angelegt.

Wird zusätzlich eine `meta_anchor.xml` verwendet, um den Vorgang zu beschreiben, so werden alle `<property>` Elemente innerhalb eines `<anchor>` Elementes angelegt.

Für einen Export werden immer nur die `<property>` Elemente aus einem der beiden Elemente verwendet.

Soll eine `goobi_exportXml.xml` Datei für verschiedene Projekte genutzt werden, die teilweise nur die `meta.xml` und teilweise auch die `meta_anchor.xml` verwenden, können problemlos beide Elemente mit ihren jeweiligen `<property>` Unterelementen angegeben werden. Diese beeinflussen sich nicht gegenseitig.