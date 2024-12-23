# config_contentServer.xml

In der Datei `config_contentServer.xml` werden technische Details zu dem von Goobi verwendeten Content Server angegeben. Diese Konfigurationsdatei kann für Goobi Workflow und Goobi Viewer gleichermaßen verwendet werden. 

Die Datei befindet sich üblicherweise an folgendem Speicherpfad:

```bash
/opt/digiverso/goobi/config/config_contentServer.xml
```

Beispielhaft sieht diese Konfigurationsdatei wie folgt aus:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<config>
	<localConfigPath value="/opt/digiverso/config/config_contentServer.xml" />
	<defaultResolution
		value="600" />
	<connectionTimeout>2000</connectionTimeout>
	<openJpeg>
		<binaries>/opt/digiverso/OpenJpeg</binaries>
	</openJpeg>
	<imageToPdfSizeFactor tiff="0.35" jpg="1.0" />
	<maxFileLength
		file=""
		value="0" />
	<scaling
		quality="QUALITY"
		thumbnailQuality="SPEED"
		maxStepSize="50" />
	<defaultFileNames>
		<image
			value="image_$datetime"
			sendAsAttachment="false" />
		<pdf
			value="ContentServer_$datetime"
			sendAsAttachment="true" />
	</defaultFileNames>
	<defaultRepositoryPathImages
		value="file:///opt/digiverso/viewer/media/" />
	<defaultRepositoryPathPdf
		usage="true"
		value="file:///opt/digiverso/viewer/pdf/" />
	<defaultRepositoryPathAlto
		usage="false"
		value="file:///opt/digiverso/viewer/alto/"
		fontFile="font.ttf" />
	<defaultRepositoryPathMets
		value="file:///opt/digiverso/viewer/mets/" />
	<defaultImageConfig defaultFormat="jpeg" />
	<defaultPdfConfig
		pagesize="A4"
		imageDpi="0"
		imageScale="1.0"
		imageScaleToBox=""
		imageCompression="0"
		convertToGrayscale="false"
		writeAsPdfA="false"
		metsFileGroup="PRESENTATION" 
		metsFileUrlRemove="file:\/\/\/opt\/digiverso\/viewer\/media\/" writeAsPdfA="false" />
	<defaultHighlightColor
		valueRed="255"
		valueGreen="255"
		valueBlue="0"
		valueAlpha="255" />
	<imageTypeSettings>
		<type format="png">
			<settings scaleWithScalr="false"></settings>
		</type>
		<type compression="jpeg" colorType="grayscale">
			<settings forceConvertToBuffered="true"></settings>
		</type>
		<type format="jpeg">
			<settings scaleWithScalr="true"></settings>
		</type>
		<type format="tiff" embeddedColorProfile="true">
			<settings scaleWithScalr="false"></settings>
		</type>
		<type format="jpg2000">
			<settings scaleWithScalr="false" allowSubSampling="true"></settings>
		</type>
		<type
			format="default"
			colorType="default"
			compression="default"
			embeddedColorProfile="both"
			minSize="0"
			maxSize="0">
			<settings
				allowRenderWithJAI="false"
				scaleWithScalr="true"
				mergeWithJAI="false"
				forceConvertToBuffered="false"
				forceConvertToRGB="false"
				forwardDirectlyIfPossible="true"
				preferredImageReader="com.github.jaiimageio"
				preferredImageWriter="com.github.jaiimageio">
			</settings>
		</type>
	</imageTypeSettings>
	<watermark
		use="false"
		scale="true"
		convertColorSpace="false"
		scaleToPercent="6"
		configFile="file:///opt/digiverso/viewer/config/config_imageFooter.xml" />
	<errorWaterMark
		title="Error"
		titleFontSize="20" 
		messageFontSize="14"
		messageMaxLineLength="60" />
	<pdfTitlePage
		use="true"
		templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
		defaultTemplate="default"
		configFile=""
		fontFile="" />
	<pdfChapterTitlePages
		use="true"
		templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
		defaultTemplate="default" />
	<singlePdfTitlePage
		use="false"
		templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
		defaultTemplate="default" />
	<restapi use="false">
		<iiif>
			<attribution></attribution>
			<logo></logo>
			<license></license>
		</iiif>
		<discloseContentLocation>true</discloseContentLocation>
	</restapi>
	<contentCache
		useCache="false"
		size="100"
		useShortFileNames="false"
		path=""
		cachePartialImages="false" />
	<thumbnailCache
		useCache="false"
		size="100"
		useShortFileNames="false"
		path="" />
	<pdfCache
		useCache="true"
		size="100"
		useShortFileNames="false" />
	<memoryUsage
		maximalParallelImageRequests="0"
		maximalParallelPdfRequests="0"
		lowMemoryShreshold="1000000000"
		memoryUnit="MB"
		timeoutUnit="s"
		triggerGCAfterAction="true">
		<image>
			<maxParallelRequests>20</maxParallelRequests>		
			<lowMemoryThreshold>200</lowMemoryThreshold>
			<lowMemoryTimeout>8</lowMemoryTimeout>
		</image>
		<pdf>
			<maxParallelRequests>8</maxParallelRequests>		
			<lowMemoryThreshold>500</lowMemoryThreshold>
			<lowMemoryTimeout>10</lowMemoryTimeout>
		</pdf>
		<metsPdf>
			<maxParallelRequests>4</maxParallelRequests>		
			<lowMemoryThreshold>1000</lowMemoryThreshold>
			<lowMemoryTimeout>20</lowMemoryTimeout>
		</metsPdf>
	</memoryUsage>
	<S3>
		<useCustom>true</useCustom>
		<Endpoint>http://192.168.178.124:9000</Endpoint>
		<AccessKeyID>24JW1VB99T8MAU94TBIC</AccessKeyID>
		<SecretAccessKey>OTrwBXGVBacVdXNSI7SKKrX8b+CqwANa5ngLZ4lB</SecretAccessKey>
	</S3>
</config>
```

## Datentypen

In dieser Konfigurationsdatei werden Einstellungen mit unterschiedlichen Datentypen vorgenommen. Zur Übersicht werden alle verwendeten Typen in der folgenden Tabelle kurz erklärt:

| Datentyp | Beispiele | Bedeutung |
| -------- | --------- | --------- |
| `boolean` | `false`, `true` | Boolscher Wert: kann wahr oder falsch sein |
| `string` | `TEXT`, `MB` | Text: kann beliebige Zeichen beinhalten |
| `integer` | `0`, `1000` | Ganzzahl: kann alle positiven oder negativen Zahlen (oder 0) beinhalten |
| `long` | `0`, `1000000000` | Große Ganzzahl: Wie `integer`, kann bedeutend größere Zahlen beinhalten, wird meistens für Millisekundenangaben und Zeitmarken verwendet |
| `float` | `0`, `1.0` | Gleitkommazahl: Kommazahl mit wenigen Stellen Präzision |
| `double` | `0`, `99.999` | Gleitkommazahl: Kommazahl mit vielen Stellen Präzision |

## Allgemeine Einstellungen und Standardwerte

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `value` | string | /opt/digiverso/config/config_contentServer.xml` | Dieser Parameter kann im Element `localConfigPath` verwendet werden und gibt den Speicherort dieser Konfigurationsdatei an. |
| `value` | integer | `72` | Dieser Parameter kann im Element `defaultResolution` verwendet werden und gibt die Standardauflösung einer Datei an. Die Auflösung ist DPI (Dots Per Inch), also Pixel pro Zoll. |
| `connectionTimeout` | integer | `2000` | Dieser Wert gibt ein Timeout an, das beim Senden von Bilddateien nicht überschritten werden darf. |
| `binaries` | string | `/opt/digiverso/OpenJpeg` | Dieses Element gibt den Pfad zu einer Bibliothek an, mit der Bilddateien verarbeitet werden sollen. |

Zusätzlich können im Element `imageToPdfSizeFactor` beliebige Parameter für Dateitypen gesetzt werden, für die ein spezieller Faktor für die Skalierung von diesem Dateityp zu einer PDF-Datei verwendet werden soll (siehe Beispiel). In dem Fall werden die Bilddateiendungen als Parametername und die Skalierungen als Wert verwendet. Eine Skalierung von 1.0 bedeutet dabei, dass die Bildgröße gleich bleibt. Werte unter 1.0 oder über 1.0 verkleinern oder vergrößern das Bild. Der Wert 0 sollte nicht verwendet werden.

Die Größe von Bilddateien kann auf dem Content-Server begrenzt werden. Folgende Parameter können im Element `maxFileLength` verwendet werden:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `value` | integer | `0` | Dieser Parameter gibt die maximale Dateigröße in Megabyte an. 0 kann angegeben werden, um die Größenbegrenzung zu deaktivieren. |
| `file` | string | | Dieser Parameter gibt eine Datei an, die im Fehlerfall (bei einer zu großen Datei) ersatzweise verwendet werden kann. |

Für verschiedene Anwendungszwecke kann es sinnvoll sein, Bilder unterschiedlich zu skalieren. Folgende Parameter können im Element `scaling` verwendet werden:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `quality` | string | `QUALITY` | Dieser Parameter gibt die Skalierungsqualität an. Es können die Werte `SPEED`, `QUALITY` und `ULTRAQUALITY` verwendet werden. |
| `thumbnailQuality` | string | `SPEED` | Dieser Parameter gibt die Skalierungsqualität für Vorschaubilder an. Es können die Werte `SPEED`, `QUALITY` und `ULTRAQUALITY` verwendet werden. |
| `maxStepSize` | integer | `50` | Dieser Parameter gibt zusätzlich einen Qualitätsfaktor für das Skalieren von Bilddateien mit der "Java Advanced Imaging" Bibliothek (JAI) an. Er kann zwischen 0 und 99 liegen. Bilddateien haben eine höhere Qualität, je höher dieser Wert ist. Ein geringerer Wert hingegen beschleunigt den Ladevorgang. Empfohlen werden Werte zwischen 10 und 50. |

Zum Herunterladen von Bildern, die im Content-Server generiert wurden, kann hier ein standardmäßiger Dateiname angegeben werden. Folgende Parameter können in den Elementen `image` und `pdf` innerhalb des Elementes `defaultFileNames` verwendet werden:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `value` | string | `image_$timestamp` für image und `ContentServer_$timestamp` für pdf | Dieser Parameter gibt an, wie ein Dateiname gebildet werden soll. Dabei kann `$timestamp` als Platzhalter für den aktuellen Zeitpunkt verwendet werden. |
| `sendAsAttachment` | boolean | `false` für image und `true` für pdf | Dieser Parameter gibt an, ob in der Serverantwort ein `attachment`-Headerfeld gesetzt werden soll. |

Für nicht-vollständige Anfragen an den Content-Server können Standard-Pfade für Speicherorte verschiedener Dateitypen angegeben werden. Folgende Parameter können in den Elementen `defaultRepositoryPathImages`, `defaultRepositoryPathPdf`, `defaultRepositoryPathAlto` und `defaultRepositoryPathMets` verwendet werden:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `usage` | boolean | `false` | Dieser Parameter kann bei den Elementen `defaultRepositoryPathPdf` und `defaultRepositoryPathAlto` verwendet werden und gibt an, ob dieser Pfad verwendet werden soll. |
| `value` | string | `file:///opt/digiverso/viewer/media/` bzw. `.../alto/` | Dieser Parameter kann bei allen Elementen verwendet werden und gibt den Pfad zu dem entsprechenden Ordner an. |
| `fontFile` | string | | Dieser Parameter kann nur bei `defaultRepositoryPathAlto` verwendet werden und gibt den Pfad zu einer Schrift-Datei an. |

Der Datentyp `image` umfasst zunächst alle Bilddateitypen, die nicht näher spezifiziert sind. Daher können mit `defaultImageConfig` Einstellungen zu Bilddateien getroffenwerden. Folgende Parameter können im Element `defaultImageConfig` verwendet werden:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `defaultFormat` | string | `jpeg` | Dieser Parameter gibt den Standard-Bildtyp an. |

PDF-Dateien werden separat konfiguriert, da sie im Gegensatz zu anderen Bilddateiformaten einige spezielle Eigenschaften haben. Folgende Parameter können im Element `defaultPdfConfig` verwendet werden:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `pagesize` | string | `A4` | Dieser Parameter gibt die Seitengröße des PDF-Dokumentes an. Mögliche Werte sind `A4`, `A4Box` und `original`. |
| `imageDpi` | float | `0` | Dieser Parameter gibt die Auflösung (Pixel pro Zoll / Dots Per Inch) an. Die Bilddateigröße (in Pixeln) bleibt dabei gleich. 0 kann angegeben werden, um die Skalierung der Auflösung zu deaktivieren. |
| `imageScale` | float | `1.0` | Dieser Parameter gibt die Bildskalierung an. 1.0 bedeutet dabei die Originalgröße. Ein Wert unter 1.0 verringert die Bildgröße, ein Wert über 1.0 vergrößert diese. Dieser Wert sollte nicht auf 0 gesetzt werden, da ansonsten das Bild verschwindet (0 Pixel Größe). |
| `imageScaleToBox` | string | | Dieser Parameter gibt an, wie die Bilddatei skaliert werden soll. In diesem Feld wird eine Kombination zweier positiver Zahlen (Breite und Höhe) erwartet. Dabei werden beide Zahlen von einem `x` getrennt und dürfen keine anderen Zeichen (z.B. Leerzeichen) beinhalten. Dieser Wert kann zum Beispiel wie folgt aussehen: `1200x900` oder `4500x2000`. |
| `imageCompression` | integer | `0` | Dieser Parameter gibt an, wie stark die Bilddatei komprimiert werden soll. 0 ist ein Standardwert, bei dem automatisch eine passende JPEG-Komprimierung ausgewählt wird. 0 sollte normalerweise immer verwendet werden. |
| `convertToGrayscale` | boolean | `false` | Dieser Parameter gibt an, ob die Bilddatei zu Graustufen konvertiert werden soll. |
| `writeAsPdfA` | boolean | `false` | Dieser Parameter gibt an, ob die Bilddatei vom Typ PDF-A sein soll. |
| `metsFileGroup` | string | `DEFAULT` | Dieser Parameter gibt an, welche Metadatengruppe verwendet werden soll. |
| `metsFileUrlRemove` | string | | In diesem Parameter kann eine URL angegeben werden, die beim Export von PDF-Dateien nicht als Bezugsquelle für Metainformationen verwendet werden soll. |

Zum Markieren verschiedener Bildelemente kann eine Farbe festgelegt werden. Folgende Parameter können im Element `defaultHighlightColor` verwendet werden:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `valueRed` | integer | `255` | Dieser Parameter gibt den Rot-Wert im Bereich von 0 bis 255 an. |
| `valueGreen` | integer | `255` | Dieser Parameter gibt den Grün-Wert im Bereich von 0 bis 255 an. |
| `valueBlue` | integer | `0` | Dieser Parameter gibt den Blau-Wert im Bereich von 0 bis 255 an. |
| `valueAlpha` | integer | `255` | Dieser Parameter gibt den Alpha-Wert (Transparenz) im Bereich von 0 bis 255 an. |

Folgende Tabelle zeigt einige einfache Farbbeispiele:

| Konfiguration | Farbe |
| ------------- | ----- |
| `valueRed="0" valueGreen="0" valueBlue="0"` | Schwarz |
| `valueRed="0" valueGreen="0" valueBlue="255"` | Blau |
| `valueRed="0" valueGreen="255" valueBlue="0"` | Grün |
| `valueRed="0" valueGreen="255" valueBlue="255"` | Cyan |
| `valueRed="255" valueGreen="0" valueBlue="0"` | Rot |
| `valueRed="255" valueGreen="0" valueBlue="255"` | Magenta |
| `valueRed="255" valueGreen="255" valueBlue="0"` | Gelb |
| `valueRed="255" valueGreen="255" valueBlue="255"` | Weiß |

Dabei bedeuten `alpha="255"` eine volle Deckkraft der Farbe (überdeckt also den Bildausschnitt komplett) und `alpha="0"` keine Deckkraft (unsichtbar).

```xml
<localConfigPath value="/opt/digiverso/config/config_contentServer.xml" />
<defaultResolution
	value="600" />
<connectionTimeout>2000</connectionTimeout>
<openJpeg>
	<binaries>/opt/digiverso/OpenJpeg</binaries>
</openJpeg>
<imageToPdfSizeFactor tiff="0.35" jpg="1.0" />
<maxFileLength
	file=""
	value="0" />
<scaling
	quality="QUALITY"
	thumbnailQuality="SPEED"
	maxStepSize="50" />
<defaultFileNames>
	<image
		value="image_$datetime"
		sendAsAttachment="false" />
	<pdf
		value="ContentServer_$datetime"
		sendAsAttachment="true" />
</defaultFileNames>
<defaultRepositoryPathImages
	value="file:///opt/digiverso/viewer/media/" />
<defaultRepositoryPathPdf
	usage="true"
	value="file:///opt/digiverso/viewer/pdf/" />
<defaultRepositoryPathAlto
	usage="false"
	value="file:///opt/digiverso/viewer/alto/"
	fontFile="font.ttf" />
<defaultRepositoryPathMets
	value="file:///opt/digiverso/viewer/mets/" />
<defaultImageConfig defaultFormat="jpeg" />
<defaultPdfConfig
	pagesize="A4"
	imageDpi="0"
	imageScale="1.0"
	imageScaleToBox=""
	imageCompression="0"
	convertToGrayscale="false"
	writeAsPdfA="false"
	metsFileGroup="PRESENTATION" 
	metsFileUrlRemove="file:\/\/\/opt\/digiverso\/viewer\/media\/" writeAsPdfA="false" />
<defaultHighlightColor
	valueRed="255"
	valueGreen="255"
	valueBlue="0"
	valueAlpha="255" />
```

## Bilddateitypen

Innerhalb des Elementes `imageTypeSettings` sind Einstellungen zu beliebig vielen Bilddateitypen definierbar. Für jeden Bilddateityp wird ein `type`-Element mit dem Unterelement `settings` angegeben.

Für Dateitypen (`type`) können folgende Parameter verwendet werden:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `format` | string | `default` | Dieser Parameter gibt den Typ der Bilddatei an. Dieser Typ entspricht der zugehörigen Dateiendung. |
| `minSize` | double | `0` | Dieser Parameter gibt an, wie groß (in Bytes) eine Bilddatei mindestens sein muss. |
| `maxSize` | double | `0` | Dieser Parameter gibt an, wie groß (in Bytes) eine Bilddatei maximal sein darf. |
| `compression` | string | `default` | Dieser Parameter gibt eine Art der Komprimierung an. |
| `colorType` | string | `default` | Dieser Parameter gibt an, auf welche Art Farbwerte gespeichert werden. |
| `embeddedColorProfile` | string | `both` | Dieser Parameter gibt ein Farbprofil an. |
| `watermark` | boolean | | Dieser Parameter gibt an, ob Wasserzeichen verwendet werden sollen. |

 **Hinweis:** Die Parameter `minSize` und `maxSize` werden in der Konfiguration als Gleitkommazahlen abgefragt, später allerdings als `long`-Zahlen weiterverarbeitet. Daher sollten nur Ganzzahlen angegeben werden.

Für Dateitypen-Einstellungen (`settings`) können folgende Parameter verwendet werden:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `preferredImageReader` | string | | Dieser Parameter gibt eine Java-Klasse an, die Bilddateien dieses Dateityps lesen kann. |
| `preferredImageWriter` | string | | Dieser Parameter gibt eine Java-Klasse an, die Bilddateien dieses Dateityps schreiben kann. |
| `mergeWithJAI` | boolean | `false` | Dieser Parameter gibt an, ob die "Java Advanced Imaging" Bibliothek (JAI) verwendet werden soll. |
| `allowRenderWithJAI` | bollean | `false` | Dieser Parameter gibt an, ob Bilder mit der "Java Advanced Imaging" Bibliothek (JAI) gerendert werden sollen. |
| `scaleWithScalr` | boolean | `false` | Dieser Parameter gibt an, ob Bilder mit dem "Scalr"-Algorithmus skaliert werden sollen. Dieser liefert nochmals bessere Ergebnisse, ist allerdings langsamer. Normalerweise sollte dieser Wert `false` sein.|
| `forceConvertToBuffered` | boolean | `false` | Dieser Parameter gibt an, ob Bilder bei der Verarbeitung gepuffert werden sollen. |
| `forceConvertToRGB` | boolean | `false` | Dieser Parameter gibt an, ob Bilder bei der Verarbeitung zu dem Farbmodell `RGB` konvertiert werden sollen. |
| `forwardDirectlyIfPossible` | boolean | `true` | Dieser Parameter gibt an, ob Bilder, die nicht mehr weiterverarbeitet werden müssen, direkt aus den Rohdaten übernommen werden sollen. Wird diese Option auf `true` gesetzt, können einige Bilddateien möglicherweise schneller abgearbeitet werden. Diese Einstellung hat den Seiteneffekt, dass einige Metainformationen von Bilddateien ohne Filterung oder Anpassung durch den Content-Server weiterverwendet werden. |
| `allowSubSampling` | boolean | `false` | Dieser Parameter gibt an, ob "SubSampling" verwendet werden soll. |

```xml
<imageTypeSettings>
	<type format="png">
		<settings scaleWithScalr="false"></settings>
	</type>
	<type compression="jpeg" colorType="grayscale">
		<settings forceConvertToBuffered="true"></settings>
	</type>
	<type format="jpeg">
		<settings scaleWithScalr="true"></settings>
	</type>
	<type format="tiff" embeddedColorProfile="true">
		<settings scaleWithScalr="false"></settings>
	</type>
	<type format="jpg2000">
		<settings scaleWithScalr="false" allowSubSampling="true"></settings>
	</type>
	<type
		format="default"
		colorType="default"
		compression="default"
		embeddedColorProfile="both"
		minSize="0"
		maxSize="0">
		<settings
			allowRenderWithJAI="false"
			scaleWithScalr="true"
			mergeWithJAI="false"
			forceConvertToBuffered="false"
			forceConvertToRGB="false"
			forwardDirectlyIfPossible="true"
			preferredImageReader="com.github.jaiimageio"
			preferredImageWriter="com.github.jaiimageio">
		</settings>
	</type>
</imageTypeSettings>
```

## Wasserzeichen

Bei der automatischen Bearbeitung und Prüfung von Bilddateien kann der Content-Server Wasserzeichen setzen. Dies sind Bilder oder Bildausschnitte, die als eine Art Identitätsinformation (des Urhebers) in das bearbeitete Bild eingesetzt werden. Wasserzeichen können mit dem Element `watermark` konfiguriert werden und folgende Parameter enthalten:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `use` | boolean | `false` | Dieser Parameter gibt an, ob Wasserzeichen verwendet werden sollen. |
| `configFile` | string | | Dieser Parameter gibt den Pfad zu einer weiteren Konfigurationsdatei für die Informationen im Wasserzeichen an. |
| `scale` | boolean | `false` | Dieser Parameter gibt an, ob Wasserzeichen skaliert werden sollen. |
| `scaleToPercent` | integer | `0` | Dieser Parameter gibt an, auf welche Größe (in Prozent) das Wasserzeichen skaliert werden soll. |
| `convertColorSpace` | boolean | `true` | Dieser Parameter kann auf `true` gesetzt werden, um automatisch Farbwerte für Wasserzeichen zu konvertieren. Diese Konvertierung konvertiert von Integer- zu Byte-Werten und sollte normalerweise keine Auswirkung auf den eigentlichen Bildinhalt haben. |

Fehler-Wasserzeichen können verwendet werden, um Fehler in Dokumenten nicht auf einer folgenden Fehler-Webseite anzugezeigen, sondern als Wasserzeichen (=Overlay) direkt in den Bilddateien einzusetzen. Diese können mit dem Element `errorWaterMark` konfiguriert werden und folgende Parameter enthalten:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `title` | string | | Dieser Parameter gibt den Titel an, der in einem Fehler-Wasserzeichen stehen soll. |
| `titleFontSize` | integer | | Dieser Parameter gibt an, welche Schriftgröße der Titel eines Fehler-Wasserzeichen haben soll. |
| `messageFontSize` | integer | `14` | Dieser Parameter gibt an, welche Schriftgröße die Fehlermeldung (`message`) des Fehler-Wasserzeichens haben soll. |
| `messageMaxLineLength` | integer | `60` | Dieser Parameter gibt an, wie viele Zeichen maximal in einer Zeile der Fehlermeldung eines Fehler-Wasserzeichens stehen sollen. |

```xml
<watermark
	use="false"
	scale="true"
	convertColorSpace="false"
	scaleToPercent="6"
	configFile="file:///opt/digiverso/viewer/config/config_imageFooter.xml" />
<errorWaterMark
	title="Error"
	titleFontSize="20" 
	messageFontSize="14"
	messageMaxLineLength="60" />
```

## PDF Titelseiten

Der Content-Server kann drei verschiedene Arten von künstlichen Titelseiten generieren und an passenden Stellen in mehrseitigen PDF-Dateien einsetzen. Künstliche Titelseiten sind Seiten, die einige Metainformationen über das danach folgende Dokument bzw. Kapitel oder Dokumentabschnitt enthalten. Metadaten werden aus METS-Dateien des entsprechenden Vorgangs gelesen. Zusätzlich ist es auch möglich, in der METS-Datei verlinkte Bildinhalte anzuzeigen. Das Layout sowie statische Inhalte der Metadatenseiten werden durch XML-Dokumente, sogenannte Templates, vorgegeben, die nach individuellen Bedürfnissen angepasst werden können.

Mit `pdfTitlePage` kann eine einmalig generierte Titelseite für das gesamte PDF-Dokument generiert werden. Sie wird vor der ersten Seite eingefügt und kann nur Informationen zum Gesamtwerk und zum obersten in der PDF-Datei enthaltenen Strukturelement enthalten.

Mit dem Element `pdfChapterTitlePages` können Titelseiten vor jedem Kapitel bzw. vor jedem Strukturelement eingefügt werden und können Informationen über das jeweilige Strukturelement und das Gesamtwerk enthalten. Diese Seiten können zum Beispiel Informationen über die Dokumentstruktur (Inhaltsverzeichnisse, Kapitel, Unterkapitel, Anhänge, usw.) enthalten.

Mit dem Element `singlePdfTitlePage` können weitere, individuelle Titelseiten in das PDF-Dokument eingebunden werden, die Informationen über besondere Stellen in z.B. einem Buch angeben. Sie kann nur Informationen über das Gesamtwerk enthalten.

Für die Generierung von zusätzlichen PDF-Titelseiten können `.fo`-Vorlagendateien verwendet werden. Diese können entweder in Server-Anfragen angegeben oder in den folgenden XML-Elementen angegeben werden.

Die angegebenen Ordner (`templateFolder`) müssen zumindest für jede aktive Metadatenseite die in `defaultTemplate` angegebene XML-Datei mit Dateiendung `.fo` enthalten, sowie die Datei `fop.xconf`, die weitere Einstellungen für die Konvertierung zur PDF-Datei mittels "Apache fop" beinhaltet. Details zu "Apache fop" sind [an dieser Stelle ](https://xmlgraphics.apache.org/fop/) zu finden.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `use` | boolean | `false` | Dieser Parameter kann bei allen Arten von Titelseiten verwendet werden und gibt an, ob diese verwendet werden soll. |
| `templateFolder` | string | `/` | Dieser Parameter kann bei allen Arten von Titelseiten verwendendet werden und gibt einen Ordner an, in dem sich eine Vorlagendatei befindet. |
| `defaultTemplate` | string | `default` | Dieser Parameter kann bei allen Arten von Titelseiten verwendet werden und gibt eine (vom Standard abweichende) Vorlage an, die verwendet werden soll. Eine Vorlagendatei hat die Dateiendung `.fo` |
| `configFile` | string | | Dieser Parameter kann nur bei `pdfTitlePage` verwendet werden und gibt den Pfad zu einer weiteren Konfigurationsdatei an. |
| `fontFile` | string | | Dieser Parameter kann nur bei `pdfTitlePage` verwendet werden und gibt den Pfad zu einer Schrift-Datei an (z.B. eine `.ttf`-Datei). |

```xml
<pdfTitlePage
	use="true"
	templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
	defaultTemplate="default"
	configFile=""
	fontFile="" />
<pdfChapterTitlePages
	use="true"
	templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
	defaultTemplate="default" />
<singlePdfTitlePage
	use="false"
	templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
	defaultTemplate="default" />
```

## REST API

Mit der REST-API können Informationen über Bilddateien am Content-Server abgefragt werden. Die Parameter `attribution`, `logo` und `license` sind zusätzliche Angaben, die optional in den Bildmetadaten der zurückgesendeten Bilddateien gesetzt werden können.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `use` | boolean | `false` | Mit diesem Parameter kann angegeben werden, ob die REST-API verwendet werden soll. |
| `attribution` | string | | Dieser Wert beinhaltet Informationen über eine IIIF-Zuschreibung. |
| `logo` | string | | Dieser Wert beinhaltet Informationen über ein IIIF-Logo. |
| `license` | string | | Dieser Wert beinhaltet Informationen über eine IIIF-Lizenz. |
| `discloseContentLocation` | boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um den Speicherpfad bzw. die URI in der Antwort der REST-API-Anfrage zum Client zu senden. |

```xml
<restapi use="false">
	<iiif>
		<attribution></attribution>
		<logo></logo>
		<license></license>
	</iiif>
	<discloseContentLocation>true</discloseContentLocation>
</restapi>
```

## Cache-Speicher

Mit Cache-Speichern können Bilddaten zwischengespeichert werden, um nicht für jede (möglicherweise identische) Anfrage sämtliche Daten neu berechnen zu müssen. Für die Verarbeitung verschiedener Dateitypen werden verschiedene Caches verwendet, die mit den folgenden XML-Elementen näher konfiguriert werden können. Dabei kann mit dem Element `contentCache` ein allgemeiner Cache für Bilddateien, mit dem Element `pdfCache` ein Cache für PDF-Dateien und mit dem Element `thumbnailCache` ein Cache für Vorschaubilder verwendet werden.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `useCache` | boolean | `false` | Dieser Parameter kann bei allen Cache-Arten verwendet werden und gibt an, ob der jeweilige Cache verwendet werden soll. |
| `size` | long | `100` | Dieser Parameter kann bei allen Cache-Arten verwendet werden und gibt die maximale Größe in Megabyte des jeweiligen Caches an. |
| `useShortFileNames` | boolean | `false` | Dieser Parameter kann bei allen Cache-Arten verwendet werden und gibt an, ob verkürzte Dateinamen verwendet werden sollen. Diese beinhalten dann nur abweichende Bestandteile des Dateipfades, werden allerdings nicht empfohlen. |
| `path` | string | | Dieser Parameter kann bei `contentCache` und `thumbnailCache` verwendet werden und gibt einen Pfad an, wo der Cache gespeichert sein soll. |
| `cachePartialImages` | boolean | `false` | Dieser Parameter kann nur bei `contentCache` verwendet werden und gibt an, ob ein Cache für Teilbilder verwendet werden soll. |

```xml
<contentCache
	useCache="false"
	size="100"
	useShortFileNames="false"
	path=""
	cachePartialImages="false" />
<thumbnailCache
	useCache="false"
	size="100"
	useShortFileNames="false"
	path="" />
<pdfCache
	useCache="true"
	size="100"
	useShortFileNames="false" />
```

## Performanz

Mit dem Element `memoryUsage` können einige Speicher- und Laufzeitbeschränkungen für den Content-Server angegeben werden. Dabei beinhaltet das Element `memoryUsage` allgemeine Einstellungen und weitere Unterelemente für bestimmte Dateitypen. Für `memoryUsage` können folgende Parameter verwendet werden:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `maximalParallelImageRequests` | integer | `0` | Dieser Parameter gibt an, wie viele Anfragen gleichzeitig für Bilddateien gesendet werden dürfen. |
| `maximalParallelPdfRequests` | integer | `0` | Dieser Parameter gibt an, wie viele Anfragen gleichzeitig für PDF-Dateien gesendet werden dürfen. |
| `lowMemoryThreshold` | long | `1000 000 000` | Dieser Parameter gibt an, wie lange die Datenübertragung aller Dateitypen maximal dauern darf. |
| `memoryUnit` | string | `B` | Dieser Parameter gibt die Maßeinheit für die Speichergrößenangaben in allen `lowMemoryThreshold`-Elementen an. |
| `timeoutUnit` | string | `MILLIS` | Dieser Parameter gibt die Maßeinheit für die Zeitangaben in allen `lowMemoryTimeout`-Elementen an. |
| `triggerGCAfterAction` | boolean | `true` | Dieser Parameter kann auf `true` gesetzt werden, um regelmäßig das Aufräumen von veralteten Daten (`Garbage Collection`) auszulösen. |

Für den Parameter `memoryUnit` gibt es einige, teils missverständliche, Werte. In der folgenden Tabelle ist jeweils angegeben, welche Werte verwendet werden können und welchen genauen numerischen Werten sie intern entsprechen.

| Maßeinheit | Faktor | Bezeichnung |
| ---------- | ------ | ----------- |
| `B` | `1` | Byte |
| `K` oder `KB` | `1000` | Kilobyte |
| `KI` oder `KIB` | `1024` | Kibibyte |
| `M` oder `MB` | `1000*1000` | Megabyte |
| `MI` oder `MIB` | `1024*1024` | Mebibyte |
| `G` oder `GB` | `1000*1000*1000` | Gigabyte |
| `GI` oder `GIB` | `1024*1024*1024` | Gibibyte |
| `T` oder `TB` | `1000*1000*1000*1000` | Terabyte |
| `TI` oder `TIB` | `1024*1024*1024*1024` | Tebibyte |

Für den Parameter `timeoutUnit` gibt es ebenfalls einige mögliche Werte. In der folgenden Tabelle ist jeweils angegeben, wie diese intern interpretiert werden:

| Maßeinheit | Faktor | Bezeichnung |
| ---------- | ------ | ----------- |
| `S` oder `SECOND` oder `SECONDS` | `1` | Eine Sekunde |
| `M` oder `MS` oder `MILLI` oder `MILLIS` | `1/1000` | Eine Millisekunde |
| `MU` oder `MICRO` oder `MICROS` | `1/1000 000` | Eine Mikrosekunde |
| `N` oder `NS` oder `NANO` oder `NANOS` | `1/1000 000 000` | Eine Nanosekunde |

Mit den Unterelementen `image`, `pdf` und `metsPdf` können spezielle Einstellungen für die entsprechenden Dateitypen vorgenommen werden. Folgende Parameter können bei allen Unterelementen gleichermaßen verwendet werden:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `maxParallelRequests` | integer | `0` | Dieser Wert gibt die maximale Anzahl an parallelen Anfragen an, die gleichzeitig gestellt werden dürfen. |
| `lowMemoryThreshold` | long | `0` | Dieser Wert gibt an, wie viele Daten maximal gleichzeitig gesendet werden sollen. Dieser Wert muss passend zum `memoryUnit`-Parameter im `memoryUsage`-Element konfiguriert werden. |
| `lowMemoryTimeout` | long | `1000` | Dieser Wert gibt an, wie lange die Datenübertragung maximal dauern darf. Dieser Wert muss passend zum `timeoutUnit`-Parameter im `memoryUsage`-Element konfiguriert werden. |

```xml
<memoryUsage
	maximalParallelImageRequests="0"
	maximalParallelPdfRequests="0"
	lowMemoryShreshold="1000000000"
	memoryUnit="MB"
	timeoutUnit="s"
	triggerGCAfterAction="true">
	<image>
		<maxParallelRequests>20</maxParallelRequests>		
		<lowMemoryThreshold>200</lowMemoryThreshold>
		<lowMemoryTimeout>8</lowMemoryTimeout>
	</image>
	<pdf>
		<maxParallelRequests>8</maxParallelRequests>		
		<lowMemoryThreshold>500</lowMemoryThreshold>
		<lowMemoryTimeout>10</lowMemoryTimeout>
	</pdf>
	<metsPdf>
		<maxParallelRequests>4</maxParallelRequests>		
		<lowMemoryThreshold>1000</lowMemoryThreshold>
		<lowMemoryTimeout>20</lowMemoryTimeout>
	</metsPdf>
</memoryUsage>
```

## S3-Speicher

Mit dem Element `S3` kann optional ein S3-Cloud-Speicher eingebunden werden, um Daten auszulagern.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `useCustom` | boolean | | Mit diesem Wert kann festgelegt werden, ob ein S3-Speicher verwendet werden soll. |
| `Endpoint` | string | | Dieser Wert gibt die Adresse (URL) des S3-Servers an. Gegebenenfalls muss auch das Protokoll (`http` oder `https`) und die Portnummer angegeben werden. |
| `AccessKeyID` | string | | Dieser Wert gibt die ID des Accounts am S3-Service an. |
| `SecretAccessKey` | string | | Dieser Wert gibt den Schlüssel / Passwort des S3-Accounts an. |

```xml
<S3>
	<useCustom>true</useCustom>
	<Endpoint>http://192.168.178.124:9000</Endpoint>
	<AccessKeyID>24JW1VB99T8MAU94TBIC</AccessKeyID>
	<SecretAccessKey>OTrwBXGVBacVdXNSI7SKKrX8b+CqwANa5ngLZ4lB</SecretAccessKey>
</S3>
```