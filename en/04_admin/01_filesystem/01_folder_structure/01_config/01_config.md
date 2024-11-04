# ‘config’ sub-directory

The `config` directory contains all the Goobi configuration files that do not have to be located within the application itself. These are listed below:

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

Depending on the specific installation, the config directory may also contain other configuration files in addition to those related to the application’s core components. Accordingly, we recommend that you also use this central configuration directory to store configurations for individual plug-ins that provide additional functionality.

```bash
plugin_abc.xml
plugin_xyz.xml
```

For subsequent ease of maintenance, the paths and file names relating to the configuration of any new Goobi plug-ins that may be developed should also adhere to this convention.