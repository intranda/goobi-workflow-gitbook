# goobi_digitalCollections.xml

The configuration file `goobi_digitalCollections.xml` is responsible for controlling the selection list of digital collections. It is usually located at the following path in the file system:

```bash
/opt/digiverso/goobi/config/goobi_digitalCollections.xml
```

In this configuration file you define which collections basically exist and within which projects they should be available for selection.

{% code title="goobi_digitalCollections.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<DigitalCollections>
	<default>
		<DigitalCollection>General</DigitalCollection>
		<DigitalCollection>Biology</DigitalCollection>
		<DigitalCollection>Physics</DigitalCollection>
		<DigitalCollection>Mathematics</DigitalCollection>
	</default>
</DigitalCollections>
```
{% endcode %}

If collections are to be configured with sub collections, these are separated from each other by the `#` separator. This looks like the following example:

{% code title="goobi_digitalCollections.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<DigitalCollections>
	<default>
		<DigitalCollection>General</DigitalCollection>
		<DigitalCollection>Biology</DigitalCollection>
		<DigitalCollection>Biology#Animals</DigitalCollection>
		<DigitalCollection>Biology#Plants</DigitalCollection>
	</default>
</DigitalCollections>
```
{% endcode %}

If the collections are to be configured differently depending on the project, this can be done as follows:

{% code title="goobi_digitalCollections.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<DigitalCollections>
  <default>
    <DigitalCollection>General</DigitalCollection>
  </default>
  <project>
    <name>Archive Project</name>
    <DigitalCollection>Monographs</DigitalCollection>
    <DigitalCollection>Files</DigitalCollection>
    <DigitalCollection>Maps</DigitalCollection>
  </project>
  <project>
    <name>Newspapers</name>
    <DigitalCollection>1920 - 1930</DigitalCollection>
    <DigitalCollection>1930 - 1940</DigitalCollection>
    <DigitalCollection>1940 - 1950</DigitalCollection>
  </project>
</DigitalCollections>
```
{% endcode %}