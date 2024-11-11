# goobi_normdata.xml

In the configuration file `goobi_normdata.xml` links to databases are specified, which can be used for universal purposes. A main application is to obtain metadata to digitized objects. The file is usually located at the following location:

```bash
/opt/digiverso/goobi/config/goobi_normdata.xml
```

For example, this configuration file looks as follows:

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

The file `goobi_normdata.xml` contains a simple list of norm databases that can be used in Goobi, for example also by plugins. For each registered database there is a `<normdatabase>` element, which contains the further information.

The parameter `url` specifies the URL of the database. This should point to an API that can be queried by Goobi. Depending on the usage or plugin, the start page of the database can also be specified here, where a user can query object data in the browser.

The `abbreviation` parameter is used to specify an abbreviation that uniquely identifies this database. The abbreviation can be used, for example, for configurations and file imports and exports.

The additional `name` parameter is not currently used by Goobi Workflow. It is used for completeness in the configuration file and contains the full, human readable, name of the database. Alternatively, a common abbreviation can be specified here. This parameter can also be used by plugins when they read the file themselves.