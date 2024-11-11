# messages_xx.properties

In the translation files `messages_xx.properties` translations for texts in the user interface are specified. The `xx` mentioned here must be replaced by the corresponding language abbreviation depending on the language used. The abbreviations are described in more detail below. The files are usually located at the following memory path:

```bash
/opt/digiverso/goobi/config/messages_xx.properties
```

Since these files become very large and often have many thousands of entries, only a few lines are given here as examples:

English translations:

{% code title="messages_en.properties" %}
```ini
...
fileHasNLines=The file has {0} lines.
next=Next >
openFile=Open File
...
```
{% endcode %}

German translations

{% code title="messages_de.properties" %}
```ini
...
fileHasNLines=Die Datei hat {0} Zeilen.
next=Weiter >
openFile=Datei \u00F6ffnen
...
```
{% endcode %}

## General

Goobi translates all texts in the user interface into the language set by the user. For this purpose, each text in Goobi has its own key, which is not displayed directly, but is searched for in the appropriate translation file. The text defined there is then displayed. The key is therefore the same for all languages, especially if additional languages are to be added.

If no entries or translations are found for a key, the key is displayed directly in the user interface. However, this is only intended for the development process. Normally all texts should be translated completely.

## Standard files and user-defined files

The default translation files used by Goobi are already included in the installation and are not relevant here. The configuration directory (by default `/opt/digiverso/goobi/config/`) is where the user-defined files are created.

## Supported languages

By default, following languages are supported:

| Abbreviation | Language       |
| ------------ | -------------- |
| `de`         | German         |
| `en`         | English        |
| `es`         | Spanish        |
| `fr`         | French         |
| `it`         | Italian        |
| `iw`         | Hebrew         |
| `nl`         | Dutch          |
| `pt`         | Portuguese     |

## Conventions for keys

* Keys must be unique. If a key is defined more than once, the wrong one may be used.
* Keys should have meaningful, but not too long names.
* Keys should be in English language.
* Multiple words in keys can be written in CamelCaseNotation (`keyWithMultipleWords`) or with underscores (`key_with_multiple_words`). Mixed forms are also common.
* Keys must not contain special characters and umlauts.
* Dots and dashes can be used without escaping.
* For translating process or step titles, spaces are often necessary in the key. These must be escaped (for example: 'import\ images').

## Prefixes for keys

If many translations belong together or are used in the same plugin, prefixes should be used in the keys. This also has the advantage that related translations are easier to find in the messages files, since they are sorted lexicographically by keys.

Frequently used prefixes are for example:

| Prefix for keys      | Example key                 | Usage     |
| -------------------- | --------------------------- | ----------- |
| `NORM_`              | `NORM_authorityData`        | Label texts for data from norm databases |
| `goobiScript_`       | `goobiScript_command`       | Texts for GoobiScripts and associated functions |
| `help_`              | `helpConfirmNewPassword`    | Help texts that explain the functions in the user interface in more detail |
| `import_`            | `import_Authors`            | Texts for import functions |
| `intranda_`          | `intranda_step_pdfUpload`   | Older convention for plugin texts |
| `lw_`                | `lw_progress`               | Texts in the LayoutWizzard |
| `mets_`              | `mets_showThisImage`        | Texts in the METS-Editor |
| `plugin_`            | `plugin_opac_json_volume`   | There are many possible prefixes for the `plugin_` prefix. For example, if translations are to be created for the `imageQA` plugin, the plugin type and plugin name are added to the plugin prefix: `plugin_intranda_step_imageQA_` |
| `process_`           | `process_created`           | Texts for processes |
| `rights_`            | `rights_Workflow_Processes` | Texts for permissions in Goobi workflow or plugins |
| `vocabularyManager_` | `vocabularyManager_type`    | Texts in the vocabulary manager |

## Conventions for texts

* The file entry for a new translation should always be added at the appropriate place in all messages files to keep the files clear and compatible. This applies in particular also if a text cannot yet be translated meaningfully into a less frequently used language.
* If a text cannot yet be translated because, for example, no suitable translator is currently available, the English translation should be entered instead.
* If a translation has not yet been confirmed by an experienced interpreter or native speaker, the suffix 'zzz' is appended to the text.

## The ending zzz

The suffix `zzz` is written as an ending to a translation to indicate that it still needs to be quality checked. This makes it easier for interpreters or native speakers to check translations, because they do not have to check all translations every time.

Goobi recognizes the ending 'zzz' by itself and displays the corresponding text without the ending.

For example, a translation may appear like this in the messages file:

```ini
choose_file=Please select a file zzz
```

## Parameters

Messages can use parameters. This makes it possible to insert values into texts without having to split the texts at each individual inserted value. Parameters only work when texts are translated into Goobi with appropriate Java functions and associated parameters. Therefore they are only used for specific purposes.

For example, a translation with parameters may look like this:

```ini
user_is_not_allowed_to_execute_goobiscript=The user {0} is not allowed to execute the goobi script {1}.
```

### Umlauts and special characters

There are some characters that must be escaped in the translations. These include some syntactic characters:

* `!` becomes `\!`
* `:` becomes `\:`
* `{` becomes `\{`
* `}` becomes `\}`
* `\` becomes `\\`

Because messages files are intended to be compatible with many languages, all special characters and umlauts are stored as Unicode sequences.

This has the advantage that files can be opened, edited and saved with any ASCII-compatible text editor without damaging the file encoding.

The disadvantage, however, is that umlauts and special characters must be entered manually as Unicode sequences.

German umlauts are given here as an example. Special characters for other languages can be taken from the Unicode character table.

* ä = `\u00E4`
* ö = `\u00F6`
* ü = `\u00FC`
* Ä = `\u00C4`
* Ö = `\u00D6`
* Ü = `\u00DC`
* ß = `\u00DF`

For example, a German translation would have to be coded as follows:

```ini
file_size=Dateigr\u00F6\u00DFe
```