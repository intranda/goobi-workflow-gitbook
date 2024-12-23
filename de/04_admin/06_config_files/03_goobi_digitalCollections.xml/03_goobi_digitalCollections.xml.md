# goobi_digitalCollections.xml

Die Konfigurationsdatei `goobi_digitalCollections.xml` ist für die Steuerung der Auswahlliste von digitalen Sammlungen zuständig. Sie befindet sich üblicherweise an folgendem Pfad im Dateisystem:

```bash
/opt/digiverso/goobi/config/goobi_digitalCollections.xml
```

In dieser Konfigurationsdatei wird festgelegt, welche Sammlungen grundsätzlich existieren, und innerhalb welcher Projekte diese zur Auswahl stehen sollen.

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

Sollen Sammlungen mit Untersammlungen konfiguriert werden, so werden diese mit dem Trennzeichen `#` voneinander getrennt. Dies sieht beispielhaft folgendermaßen aus:

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

Sollen die Sammlungen je nach Projekt unterschiedlich konfiguriert werden, so kann dies folgendermaßen erfolgen:

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