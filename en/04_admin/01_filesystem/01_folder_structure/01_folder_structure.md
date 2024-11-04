# Global directory structure

As a web-based application, Goobi has its own structure and is located on a defined path in the file system independently of the servlet container being used. This section explains how to organise the directory structures within which Goobi saves its data and the different configuration files.

The base path for all digitisation software in the Goobi environment is:

```bash
/opt/digiverso/
```

The following directories are usually located on this base path:

```bash
/opt/digiverso/goobi/
/opt/digiverso/logs/
/opt/digiverso/itm/
/opt/digiverso/viewer/
```

The `logs` directory is the main directory for log files. Goobi log files are also stored here \(assuming the system is properly configured\). The other directories listed above relate to frequently used applications \(e.g. `viewer` for the Goobi viewer, `itm` for the intranda Task Manager and `goobi` for Goobi.

The base path for Goobi is:

```bash
/opt/digiverso/goobi/
```

In most cases, this base path will accommodate the following folder structure \(see below for details of each sub-directory\):

```bash
/opt/digiverso/goobi/config/
/opt/digiverso/goobi/import/
/opt/digiverso/goobi/metadata/
/opt/digiverso/goobi/plugins/
/opt/digiverso/goobi/rulesets/
/opt/digiverso/goobi/scripts/
/opt/digiverso/goobi/xslt/
```