# goobi_processProperties.xml

In der Konfigurationsdatei `goobi_processProperties.xml` können weitere Eigenschaften für Projekte, Vorgänge und Schritte angegeben werden. Die Datei befindet sich üblicherweise an folgendem Speicherpfad:

```bash
/opt/digiverso/goobi/config/goobi_processProperties.xml
```

Beispielhaft sieht diese Konfigurationsdatei wie folgt aus:

{% code title="goobi_processProperties.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<config_processProperties>
	<property name="Example" container="0">
		<project>Project 1</project>
		<project>Project 2</project>
		<workflow>Workflow 1</workflow>
		<workflow>Workflow 2</workflow>
		<showStep name="Scanning" access="READ" duplicate="" />
		<showStep name="Check resolution" access="WRITE" duplicate="" />
		<showProcessCreation template="*" access="write">
          <display property="Resolution" value="undefined" />
        </showProcessCreation>
		<showProcessGroup access="write" />
		<validation>\w</validation>
		<type>LIST</type>
		<defaultvalue>Please select...</defaultvalue>
		<value>Value 1</value>
		<value>Value 2</value>
	</property>
</config_processProperties>
```
{% endcode %}

## Allgemeines

Mit jedem `<property>` Block wird eine Eigenschaft definiert. Diese kann so konfiguriert werden, dass sie für ein oder mehrere Projekte, ein oder mehrere Vorgänge oder einen oder mehrere Schritte gilt. Kombinationen sind ebenfalls möglich. Statt einem Projektnamen, Vorgangstitel oder Schritttitel kann ein Sternchen (`*`) verwendet werden, um alle Projekte, Vorgänge oder Schritte anzusprechen.

Für jede `<property>` wird mit dem Parameter `name` ein Name angegeben, dieser sollte eindeutig und aussagekräftig sein.

Für jede `<property>` wird mit dem Parameter `container` ein Container angegeben, in die die definierte Eigenschaft intern eingeordnet werden soll.

## Verfügbare Konfigurationen

Als Unterelemente stehen für das `<property>` Tag folgende Tags zur Verfügung:

| Tag                  | Mehrfach anwendbar        | Beschreibung |
| -------------------- | ------------------------- | ----------------------- |
| `<project>`          | ja                        | Mit diesem Element können ein oder mehrere Projekte angegeben werden, für das/die die Eigenschaft gelten soll. Alternativ kann ein Sternchen (`*`) verwendet werden, um alle Projekte anzusprechen. |
| `<workflow>`         | ja                        | Mit diesem Element können ein oder mehrere Produktionsvorlagen angegeben werden, für das/die die Eigenschaft gelten soll. Alternativ kann ein Sternchen (`*`) verwendet werden, um für alle Produktionsvorlagen zu gelten. |
| `<showStep>`         | ja                        | Mit diesem Element wird angegeben, dass ein einzelner Schritt in der Benutzeroberfläche angezeigt wird. Mit dem `name` Parameter wird der Schritttitel angegeben. Mit dem `access` Parameter wird ein Zugriffsrecht angegeben, siehe unten. Mit dem `duplicate` Paramter wird angegeben, ob Schritte mehrfach vorkommen dürfen. |
| `<showProcessCreation>`| ja                      | Mit diesem Element kann definiert werden, dass die Eigenschaft in der Anlegemaske angezeigt wird. |
| `<showProcessGroup>` | nein                      | In diesem Element wird mit dem Parameter `access` ein Zugriffsrecht für Gruppen von Vorgängen definiert. Für Details, siehe unten. |
| `<validation>`       | nein                      | Mit diesem Element können Parameter für eine Validierung angegeben werden. |
| `<type>`             | nein                      | Dieses Element spezifiziert den Datentyp dieser Eigenschaft. Für unterstützte Datentypen, siehe unten. |
| `<defaultvalue>`     | nein                      | Dieses Element spezifiziert den Standardwert eines Input-Feldes oder einer Auswahl. |
| `<value>`            | bei Listen ja, sonst nein | Bei einfachen Eingabefeld-Typen gibt dieses Element einen vordefinierten Wert an. Bei Listen geben mehrere `<value>` Elemente eine Liste von auswählbaren Einträgen an. |

### Verfügbare Zugriffsrechte

<!--- Hinweis für Entwickler: Die Zugriffsrechte werden in dem Enum org.goobi.production.properties.AccessCondition definiert. -->

Alle Zugriffsrechte können in beliebiger Großschreibung geschrieben werden, diese wird beim Einlesen ignoriert.

Ist kein Wert angegeben oder wird er falsch geschrieben, so ist `READ` der Standardwert.

| Zugriffsrecht   | Beschreibung                                            |
| --------------- | ----------------------------------- |
| `READ`          | Auf die Eigenschaft kann lesend zugegriffen werden.     |
| `WRITE`         | Auf die Eigenschaft kann schreibend zugegriffen werden. |
| `WRITEREQUIRED` | Die Eigenschaft muss individuell gesetzt werden.        |

### Verfügbare Datentypen

<!--- Hinweis für Entwickler: Die Datentypen werden in dem Enum org.goobi.production.properties.Type definiert. -->

Alle Datentypen können in beliebiger Großschreibung geschrieben werden, diese wird beim Einlesen ignoriert.

Ist kein Wert angegeben oder wird er falsch geschrieben, so ist `TEXT` der Standardwert.

| Datentyp          | Beschreibung |
| ----------------- | ------------ |
| `BOOLEAN`         | Es kann ein boolscher Wert angegeben werden. Gültige Werte sind `true` und `false`. |
| `DATE`            | Es kann ein Datum ausgewählt werden. |
| `HTML`            | Ein HTML codierter Text kann verwendet werden. Abhängig vom verwendeten Internetbrowser werden alle üblichen HTML-Tags unterstützt. |
| `LINK`            | Eine URL kann verwendet werden. Diese sollte existieren und frei zugänglich sein. |
| `LIST`            | Aus einer Liste von Auswahlmöglichkeiten kann ein Element ausgewählt werden. |
| `LISTMULTISELECT` | Aus einer Liste von Auswahlmöglichkeiten können beliebig viele Elemente ausgewählt werden. |
| `METADATA`        | Es können weitere Metadaten angegeben werden. |
| `NUMBER`          | Eine Zahl kann angegeben werden. |
| `TEXT`            | Ein beliebiger Text kann verwendet werden. Dieser Text unterstützt kein HTML. |

Bei den Datentypen `LIST` und `LISTMULTISELECT` kann als Standardwert mit dem `<defaultvalue>` Tag ein Text wie zum Beispiel `Bitte auswählen` oder einer der angegebenen Werte angegeben werden. Sofern das Feld erforderlich ist, muss später einer der angegebenen Werte ausgewählt werden, auch wenn der Wert in `<defaultvalue>` abweicht.

## Besonderheiten bei Vorgängen

Es gibt zwei Fälle, in denen die in dieser Datei definierten Eigenschaften abgefragt werden. Es werden entweder Informationen über Vorgänge oder über Schritte abgefragt.

Im Falle eines Vorgangs werden nicht alle Unterelemente verwendet. Es werden nur die im folgenden Beispiel gezeigten Elemente beachtet:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<config_processProperties>
	<property name="Example" container="0">
		<project>Project 1</project>
		<project>Project 2</project>
		<showProcessGroup access="write" />
		<validation>\w</validation>
		<type>LIST</type>
		<defaultvalue>Please select...</defaultvalue>
		<value>Value 1</value>
		<value>Value 2</value>
	</property>
</config_processProperties>
```

Die Elemente `<workflow>` und `<showStep>` werden bei Vorgängen nicht verwendet.

## Bedingte Anzeige von Eigenschaften

Eigenschaften können auch bedingt angezeigt werden. Hierzu kann definiert werden, dass eine andere Eigenschaft einen bestimmten Wert haben muss, um die Anzeige damit zu steuern. Das folgende Beispiel verdeutlicht dies:

```xml
	<property name="Resolution" container="Images">
        <project>*</project>
        <showProcessCreation template="*" access="writeRequired"/>
        <type>List</type>
        <value>300</value>
        <value>400</value>
        <value>600</value>
        <value>Other</value>
    </property>
    <property name="Special Resolution" container="Images">
        <project>*</project>
        <showProcessCreation template="*" access="write">
        	<display property="Resolution" value="Other" />
        </showProcessCreation>
		<showStep name="Scanning preparation" access="write">
		    <display property="Resolution" value="Other" />
		</showStep>
        <type>Text</type>
    </property>
```

Die Eigenschaft `Special Resolution` wird hier sowohl in der Anlegemaske als auch in der Aufgabe `Scanning preparation` nur angezeigt, wenn in der Eigenschaft `Resolution` aus der Liste der Wert `Other` gewählt wurde. Im Falle eines anderen Wertes in der Eigenschaft `Resolution` ist das Textfeld `Special Resolution` nicht sichtbar.