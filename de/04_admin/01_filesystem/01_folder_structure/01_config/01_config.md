# Unterverzeichnis ‚config’

Innerhalb des Verzeichnisses `config` befinden sich sämtliche Konfigurationsdateien von Goobi, die sich nicht innerhalb der Applikation selbst befinden müssen. An dieser Stelle finden sich daher die folgenden Konfigurationsdateien:

```bash
config_contentServer.xml
goobi_activemq.xml
goobi_config.properties
goobi_digitalCollections.xml
goobi_exportXml.xml
goobi_mail.xml
goobi_metadataDisplayRules.xml
goobi_normdata.xml
goobi_opac.xml
goobi_opacUmlaut.txt
goobi_processProperties.xml
goobi_projects.xml
goobi_rest.xml
goobi_webapi.xml
messages_de.properties
messages_en.properties
```

Neben den Konfigurationsdateien für die Kernkomponenten von Goobi befinden sich je nach individueller Installation an dieser Stelle unter Umständen auch noch weitere Konfigurationsdateien. Konfigurationen für einzelne Plugins, die die Funktionalität von Goobi erweitern, sollten entsprechend ebenfalls innerhalb dieses zentralen Konfigurationsverzeichnisses vorgehalten werden.

```bash
plugin_abc.xml
plugin_xyz.xml
```

Neue Entwicklungen von zusätzlichen Goobi-Plugins sollten sich mit ihren Pfaden und Dateibenennungen für ihre Konfigurationen auch an diese Konvention halten, um eine möglichst einfache Wartung der Software zu gewährleisten.