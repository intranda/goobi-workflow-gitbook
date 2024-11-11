# Export configuration in the Goobi configuration file

A further export setting can be configured in `goobi_config.properties`. The corresponding parameter is shown below:

```ini
exportWithoutTimeLimit=true|false
```

If this value is set to `true`, Goobi will produce a success message for the export once the exported files have been copied to the folders `DMS export folder for XML file` and `DMS export folder for images` (as defined in the project settings). Goobi will produce an error message if an error occurs during the copying process.

If the value is set to `false` (or if it is missing from the configuration file), Goobi will not produce a success message unless it can find a corresponding message in the folder `DMS export success folder` (as defined in the project settings). Goobi will produce an error message if it finds an error message in the folder `DMS export error folder` (as defined in the project settings). 

If Goobi does not find a success of error message in these folders within the timeout period stipulated in the project settings, it will delete the exported items automatically.