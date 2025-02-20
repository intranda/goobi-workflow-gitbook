# messages_xx.properties

In den Übersetzungsdateien `messages_xx.properties` werden Übersetzungen für Texte in der Benutzeroberfläche angegeben. Das hier genannte `xx` muss je nach verwendeter Sprache durch das dazugehörige Sprachkürzel ersetzt werden. Die Kürzel sind unten näher beschrieben. Die Dateien befinden sich üblicherweise an folgendem Speicherpfad:

```bash
/opt/digiverso/goobi/config/messages_xx.properties
```

Da diese Dateien sehr groß werden und oftmals viele Tausend Einträge haben, sind hier nur wenige Zeilen beispielhaft angegeben:

Englische Übersetzungen:

{% code title="messages_en.properties" %}
```ini
...
fileHasNLines=The file has {0} lines.
next=Next >
openFile=Open File
...
```
{% endcode %}

Deutsche Übersetzungen:

{% code title="messages_de.properties" %}
```ini
...
fileHasNLines=Die Datei hat {0} Zeilen.
next=Weiter >
openFile=Datei \u00F6ffnen
...
```
{% endcode %}

## Allgemeines

Goobi übersetzt alle Texte in der Benutzeroberfläche in die vom Nutzer eingestellte Sprache. Dafür hat jeder Text in Goobi einen eigenen Key, der nicht direkt angezeigt, sondern in der passenden Übersetzungsdatei gesucht wird. Der dort definierte Text wird dann angezeigt. Der Key ist somit für alle Sprachen gleich, insbesondere auch dann, wenn weitere Sprachen hinzugefügt werden sollen.

Werden keine Einträge bzw. Übersetzungen für einen Key gefunden, so wird der Key direkt in der Benutzeroberfläche angezeigt. Dies ist allerdings nur für den Entwicklungsvorgang gedacht. Normalerweise sollten alle Texte vollständig übersetzt werden.

## Standard-Dateien und Benutzerdefinierte Dateien

Die standardmäßig von Goobi verwendeten Übersetzungsdateien sind bereits in der Installation enthalten und hier nicht weiter relevant. Im Konfigurationsverzeichnis (standardmäßig `/opt/digiverso/goobi/config/`) werden die benutzerdefinierten Dateien angelegt.

## Unterstützte Sprachen

Standardmäßig werden folgende Sprachen unterstützt:

| Kürzel | Sprache        |
| ------ | -------------- |
| `de`   | Deutsch        |
| `en`   | Englisch       |
| `es`   | Spanisch       |
| `fr`   | Französisch    |
| `it`   | Italienisch    |
| `iw`   | Hebräisch      |
| `nl`   | Niederländisch |
| `pt`   | Portugiesisch  |

## Konventionen für Keys

* Keys müssen eindeutig sein. Wird ein Key mehrmals definiert, kann es dazu kommen, dass der falsche verwendet wird.
* Keys sollten aussagekräftige, aber nicht zu lange Namen haben.
* Keys sollten englischsprachig sein.
* Mehrere Wörter in Keys können in CamelCaseNotation (`keyWithMultipleWords`) oder mit Unterstrichen (`key_with_multiple_words`) geschrieben werden. Mischformen sind ebenfalls üblich.
* Keys dürfen keine Sonderzeichen und Umlaute beinhalten.
* Punkte und Bindestriche können ohne Escaping verwendet werden.
* Für das Übersetzen von Vorgangs- oder Schritttiteln sind desöfteren Leerzeichen im Key notwendig. Diese müssen escaped werden (zum Beispiel: `Import\ der\ Bilder`)

## Präfixe für Keys

Wenn viele Übersetzungen zusammengehören oder im selben Plugin verwendet werden, sollten Präfixe in den Keys verwendet werden. Dies hat auch den Vorteil, dass zusammengehörige Übersetzungen in den messages-Dateien besser zu finden sind, da diese nach Keys lexikografisch sortiert sind.

Häufig verwendete Präfixe sind zum Beispiel:

| Präfix für Keys      | Beispiel Key                | Anwendung |
| -------------------- | --------------------------- | ------------------------------------------------ |
| `NORM_`              | `NORM_authorityData`        | Beschriftungstexte für Daten aus Normdatenbanken |
| `goobiScript_`       | `goobiScript_command`       | Texte für GoobiScripts und dazugehörige Funktionen |
| `help_`              | `helpConfirmNewPassword`    | Hilfe-Texte, die die Funktionen in der Benutzeroberfläche näher erklären |
| `import_`            | `import_Authors`            | Texte für Import-Funktionen |
| `intranda_`          | `intranda_step_pdfUpload`   | Ältere Konvention für Plugin-Texte |
| `lw_`                | `lw_progress`               | Texte im LayoutWizzard |
| `mets_`              | `mets_showThisImage`        | Texte im METS-Editor |
| `plugin_`            | `plugin_opac_json_volume`   | Beim `plugin_`-Präfix gibt es viele mögliche Präfixe. Sollen zum Beispiel Übersetzungen für das `imageQA`-Plugin angelegt werden, so wird der Plugin-Präfix um den Plugin-Typ und den Plugin-Namen ergänzt: `plugin_intranda_step_imageQA_` |
| `process_`           | `process_created`           | Texte für Vorgänge |
| `rights_`            | `rights_Workflow_Processes` | Texte für Berechtigungen in Goobi Workflow oder Plugins |
| `vocabularyManager_` | `vocabularyManager_type`    | Texte im Vokabelmanager |

## Konventionen für Texte

* Der Dateieintrag für eine neue Übersetzung sollte immer in allen messages-Dateien an der passenden Stelle hinzugefügt werden, um die Dateien übersichtlich und kompatibel zu halten. Dies gilt insbesondere auch dann, wenn ein Text noch nicht sinnvoll in eine seltener verwendete Sprache übersetzt werden kann.
* Kann ein Text noch nicht übersetzt werden, weil zum Beispiel zur Zeit kein geeigneter Übersetzer zur Verfügung steht, sollte stattdessen die englische Übersetzung eingetragen werden.
* Ist eine Übersetzung noch nicht durch einen erfahrenen Dolmetscher oder Muttersprachler bestätigt worden, so wird die Endung `zzz` an den Text angehangen.

## Die Endung zzz

Die Endung `zzz` wird als Endung an eine Übersetzung geschrieben, um zu signalisieren, dass diese noch qualitativ überprüft werden muss. Dies vereinfacht die Überprüfung der Übersetzungen für Dolmetscher oder Muttersprachler, weil so nicht jedes Mal alle Übersetzungen überprüft werden müssen.

Goobi erkennt die Endung `zzz` selbstständig und zeigt den entsprechenden Text ohne die Endung an.

Eine Übersetzung kann zum Beispiel so in der messages-Datei stehen:

``` toml
choose_file=Please select a file zzz
```

## Parameter

Messages können Parameter verwenden. Damit ist es möglich, Werte in Texte einzusetzen, ohne die Texte an jedem einzelnen eingesetzten Wert aufspalten zu müssen. Parameter funktionieren nur, wenn Texte mit passenden Java-Funktionen und zugehörigen Parametern in Goobi übersetzt werden. Daher werden sie nur für bestimmte Zwecke verwendet.

Eine Übersetzung mit Parametern kann zum Beispiel so aussehen:

```ini
user_is_not_allowed_to_execute_goobiscript=The user {0} is not allowed to execute the goobi script {1}.
```

### Umlaute und Sonderzeichen

Es gibt einige Zeichen, die in den Übersetzungen escaped werden müssen. Dazu gehören einige syntaktische Zeichen:

* `!` wird zu `\!`
* `:` wird zu `\:`
* `{` wird zu `\{`
* `}` wird zu `\}`
* `\` wird zu `\\`

Weil messages-Dateien kompatibel zu vielen Sprachen sein sollen, werden alle Sonderzeichen und Umlaute als Unicode-Sequenzen gespeichert.

Dies hat den Vorteil, dass Dateien mit jedem ASCII-kompatiblen Texteditor geöffnet, bearbeitet und gespeichert werden können, ohne dass die Dateicodierung beschädigt wird.

Der Nachteil ist allerdings, dass Umlaute und Sonderzeichen manuell als Unicode-Sequenzen eingegeben werden müssen.

Beispielhaft sind hier die deutschen Umlaute angegeben. Sonderzeichen für andere Sprachen können der Unicode-Zeichentabelle entnommen werden.

* ä = `\u00E4`
* ö = `\u00F6`
* ü = `\u00FC`
* Ä = `\u00C4`
* Ö = `\u00D6`
* Ü = `\u00DC`
* ß = `\u00DF`

Eine deutsche Übersetzung müsste beispielsweise wie folgt codiert werden:

```ini
file_size=Dateigr\u00F6\u00DFe
```