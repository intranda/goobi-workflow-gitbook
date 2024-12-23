# goobi_normdata.xml

In der Konfigurationsdatei `goobi_normdata.xml` werden Verlinkungen zu Datenbanken angegeben, die für universelle Zwecke verwendet werden können. Eine Hauptanwendung ist das Beziehen von Metadaten zu digitalisierten Objekten. Die Datei befindet sich üblicherweise an folgendem Speicherpfad:

```bash
/opt/digiverso/goobi/config/goobi_normdata.xml
```

Beispielhaft sieht diese Konfigurationsdatei wie folgt aus:

{% code title="goobi_normdata.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<normdatabases>
    <normdatabase name="goobi" url="https://goobi.intranda.com/" abbreviation="" />
    <normdatabase name="kulturnav" url="https://kulturnav.org/" abbreviation="kulturnav" />
    <normdatabase name="GND" url="http://d-nb.info/gnd/" abbreviation="gnd" />
    <normdatabase name="geonames" url="http://www.geonames.org/" abbreviation="geonames" />
    <normdatabase name="dante" url="https://dante.gbv.de/" abbreviation="dante" />
    <normdatabase name="viaf" url="http://www.viaf.org/viaf/" abbreviation="viaf" />
    <normdatabase name="easydb" url="https://easydb.prizepapers.gbv.de/" abbreviation="easydb" />
<!--
    <normdatabase name="REFGEO" url="http://normdata.intranda.com/normdata/refgeo/" abbreviation="intranda Geo Datenbank" />
    <normdatabase name="REFBIO" url="http://normdata.intranda.com/normdata/refbio/" abbreviation="intranda PND" />
    <normdatabase name="RVK" url="http://rvk.uni-regensburg.de/index.php?option=com_rvko&amp;view=show&amp;mode=searchNotation&amp;rvkoNotationKey=" abbreviation="rvk" />
-->
</normdatabases>
```
{% endcode %}

Die Datei `goobi_normdata.xml` beinhaltet eine einfache Liste von Normdatenbanken, die in Goobi, zum Beispiel auch von Plugins, verwendet werden können. Es exisistiert für jede eingetragene Datenbank ein `<normdatabase>` Element, das die weiteren Informationen beinhaltet.

Mit dem Parameter `url` wird die URL der Datenbank angegeben. Diese sollte auf eine von Goobi abfragbare API verweisen. Je nach Anwendung oder Plugin kann hier auch die Startseite der Datenbank angegeben werden, auf der ein Nutzer im Browser Objektdaten abfragen kann.

Mit dem Parameter `abbreviation` wird eine Abkürzung angegeben, die diese Datenbank eindeutig identifiziert. Die Abkürzung kann zum Beispiel für Konfigurationen und Dateiimporte und -Exporte verwendet werden.

Der zusätzliche Parameter `name` wird derzeit von Goobi Workflow nicht verwendet. Er dient der Vollständigkeit in der Konfigurationsdatei und beinhaltet den vollständigen, für Menschen lesbaren, Namen der Datenbank. Alternativ kann hier auch eine gebräuchliche Abkürzung angegeben werden. Dieser Parameter kann auch von Plugins verwendet werden, wenn diese die Datei selbst auslesen.