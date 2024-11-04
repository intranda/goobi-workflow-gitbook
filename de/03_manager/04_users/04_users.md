# Benutzer

Wählen Sie in der Menüleiste unter dem Menüpunkt `Administration` den Punkt `Benutzer` aus, um all diejenigen Benutzer zu verwalten, die mit Ihrem Goobi arbeiten sollen. Sie erhalten zunächst eine Übersicht über all diejenigen Benutzer, die bereits in Goobi angelegt sind. In der Spalte `Benutzer` wird Ihnen hier der ausgeschriebene Vor- und Nachnamen jedes erfassten Benutzers angezeigt. Die Spalte `Standort` liefert Ihnen Informationen, in welcher Einrichtung oder Stadt der Benutzer sich befindet. In der Spalte `Benutzergruppen` erfolgt ein Überblick darüber, in welchen Benutzergruppen die jeweilige Person Mitglied ist. Innerhalb der Spalte `Projekte` wird ersichtlich, innerhalb welcher Projekte die einzelnen Nutzer als Projektmitglied eingetragen sind.

In der Spalte `Aktionen` besteht die Möglichkeit, einen einzelnen Benutzer zu bearbeiten. Auch haben Sie an dieser Stelle als Administrator die Gelegenheit, in die Rolle eines ausgewählten Benutzers zu wechseln.

| Icon | Beschreibung |
| :--- | :--- |
| ![ruleset\_02.png](ruleset_02.png) | Neuen Benutzer anlegen |
| ![ruleset\_01.png](ruleset_01.png) | Bestehenden Benutzer bearbeiten |
| ![ruleset\_03.png](ruleset_03.png) | Wechsel in die Rolle des ausgewählten Benutzers |

Klicken Sie für diesen Rollenwechsel einfach auf das Icon `Benutzerprofil laden` in der Spalte `Aktionen`. Dadurch ändern Sie als Administrator Ihre Rechte sowie Ihre Rolle zu derjenigen der ausgewählten Person. Auf diese Weise ist es Ihnen möglich, für Testzwecke zu prüfen, wie sich Goobi für einen einzelnen bestimmten Nutzer verhält. Dies könnte insbesondere dann sinnvoll sein, wenn einzelne Benutzer über Probleme berichten, die sich nicht nachvollziehen lassen. Der Wechsel in die Rolle und die Rechte eines spezifischen Benutzers erlaubt Ihnen, die Oberflächen in exakt der gleichen Weise vorzufinden wie der Benutzer sie sieht, ohne dass dieser Ihnen seine Zugriffsdaten, insbesondere sein Passwort, nennen muss.

Oberhalb der Auflistung aller Benutzer bietet Goobi Ihnen die Möglichkeit, die Anzeige der aktuellen Nutzer zu erweitern, indem auch diejenigen Benutzer angezeigt werden können, deren Status auf inaktiv gesetzt wurde. Klicken Sie hierfür auf die Checkbox `Nur aktive Nutzer zeigen` und deaktivieren Sie somit die Einschränkung auf die aktiven Nutzer.

Der Filter oberhalb der Tabelle erlaubt Ihnen, auch in umfangreichen Benutzerauflistungen einen bestimmten Benutzer schnell aufzufinden. Geben Sie hierzu einfach einen Teil des Vor- oder Nachnamens ein und bestätigen Sie Ihre Eingabe anschließend mit der Eingabetaste.

![Auflistung der in Goobi eingetragenen Benutzer](30-61d.png)

Möchten Sie einen neuen Benutzer in Goobi hinzufügen, klicken Sie auf den Link `Neuen Benutzer anlegen` unterhalb der tabellarischen Auflistung. Möchten Sie einen bereits vorhandenen Benutzer von Goobi bearbeiten, so klicken Sie auf das erste Icon der Spalte `Aktionen` des gewünschten Benutzers.

![Bearbeitung von Benutzerdetails](30-62d.png)

In der Maske für die Bearbeitung eines einzelnen Benutzers haben Sie die Möglichkeit sämtliche Details der gewünschten Person zu bearbeiten. Neben dem `Nachnamen`, dem `Vornamen` und dem `Standort` vergeben Sie an dieser Stelle ebenfalls einen `Login`, der in Goobi verwendet werden soll, sowie ein `Passwort`.

Sofern Goobi in der Hauptkonfiguration so eingestellt wurde, dass Goobi die Benutzer gegen einen konfigurierten LDAP authentifiziert, muss für jeden einzelnen Benutzer hier festgelegt werden, welcher LDAP-Server für die Authentifizierung verwendet werden soll.

In dem Eingabefeld für die Sprache der Metadaten kann als Freitext ein Sprachcode verwendet werden. Bitte beachten Sie hierfür, dass der verwendete Sprachcode exakt mit demjenigen übereinstimmen muss, der innerhalb des Regelsatzes definiert wurde, mit dem der Benutzer im Goobi-METS-Editor arbeiten wird. Im Fall der folgenden Abbildung muss entsprechend in den Regelsätzen eine Lokalisierung der Metadaten- und Strukturdatenbezeichnungen \(`language`\) für die Sprache Englisch mit dem Sprachcode `en` vorhanden sein. Wenn das Feld leer gelassen wird, wird im Metadateneditor die Sprache des Browsers benutzt.

**Lokalisierung des Metadatums 'logicalPageNumber' für mehrere Sprachen innerhalb eines Regelsatzes**

```markup
<MetadataType>
    <Name>logicalPageNumber</Name>
    <language name="de">logische Seitenzahl (gedruckte Seitenzahl)</language>
    <language name="en">logical page number</language>
    <language name="es">número de página lógico</language>
</MetadataType>
```

Legen Sie in der Maske zur Bearbeitung des Benutzers ebenfalls fest, ob das Benutzerkonto des Benutzers aktiv oder inaktiv sein soll. Sie können somit konfigurieren, dass bereits bestehende Benutzerkonten zwar weiterhin in Goobi erhalten bleiben, die jeweiligen einzelnen Benutzer jedoch keinen weiteren Zugriff mehr auf ihren Benutzeraccount in Goobi haben sollen.

Dies ist insbesondere dafür wichtig, dass bestehende Informationen aus bereits bearbeiteten Werken und auch statistische Abfragen nicht beeinträchtigt werden, indem einzelne Nutzer aus der Datenbank gelöscht werden. Somit gewährleisten Sie, dass auch in Zukunft Informationen über Werke, deren Workflow bereits vor längerer Zeit abgeschlossen wurde, genau analysiert werden können und auch ermittelt werden kann, welche Person wann einen bestimmten Arbeitsschritt durchgeführt hat. Dies könnte insbesondere im Fehlerfall eine große Hilfe sein.

Die Checkbox `Massendownload` ermöglicht für einen einzelnen Benutzer ein besonderes Verhalten in Goobi für die Bearbeitung der eigenen Aufgaben. Sie erlaubt, dass ein Benutzer innerhalb der eigenen Aufgaben unterhalb der Auflistung der eigenen Aufgaben eine umfangreichere Liste an möglichen Aktionen erhält, die es dem Benutzer erlaubt, mit nur einem Klick gleichzeitig mehrere einzelne Aufgaben gemeinsam anzunehmen und sie beispielsweise im automatisierten Verfahren zusammen zu bearbeiten.

Nach Abschluss solcher Arbeiten, dies könnte zum Beispiel eine automatisierte Imageoptimierung im Batchbetrieb sein, verschiebt der jeweilige Benutzer innerhalb seines Arbeitsverzeichnisses, die Bände in das von Goobi bereitgestellte Verzeichnis für den Massenupload. Häufig heißt dieses Verzeichnis `fertig`, `done` oder ähnlich. Dies kann in jeder Goobi-Installation individuell konfiguriert werden.

Durch das Verschieben mehrerer Verzeichnisse zugehöriger Aufgaben in das Massenupload-Verzeichnis kann der Benutzer durch nur einen einzigen Klick innerhalb der möglichen Aktionen sämtliche bereitgestellte Aufgaben abschließen, für die sich ein zugehöriger Ordner im Massenupload-Verzeichnis befindet. Somit erlaubt Goobi dem Benutzer auch große Mengen an Aufgaben gemeinsam anzunehmen und abzuschließen.

Mit seinem granularen Rechtesystem gewährleistet Goobi, dass jede Person nicht nur in einzelnen Projekten Mitglied ist, sondern auch, dass jeder Nutzer in unterschiedlichen Rollen in Goobi unterwegs sein kann. Dabei kann jede Person zugleich mehrere Rollen wahrnehmen. Rollen lassen sich in diesem Zusammenhang auch verstehen als Qualifikation oder Fertigkeit. Welche Rollen in Goobi definiert wurden, lässt sich im Bereich der Benutzergruppen festlegen. Klicken Sie für den ausgewählten Benutzer einfach auf den Button `Benutzergruppen hinzufügen`, um dem Benutzer weitere Rollen zuzuweisen.

![Hinzuf&#xFC;gen von Benutzergruppen zur ausgew&#xE4;hlten Person](30-63d.png)

Wählen Sie in dem geöffneten Dialogfenster nun all diejenigen Benutzergruppen aus, die sie dem Benutzer zuordnen möchten, und klicken Sie auf das entsprechende Icon, um die Auswahl zu übernehmen. Nachfolgend sehen Sie, dass der Benutzer diesen Benutzergruppen zugewiesen wurde. In gleicher Weise verfahren Sie ebenfalls mit den Projekten, in denen der aktuell ausgewählte Benutzer Mitglied sein soll.

![Hinzuf&#xFC;gen von Projekten zu einem Benutzer](30-64d.png)

Möchten Sie die Person aus einer einzelnen Benutzergruppe oder Projekt entfernen, so klicken Sie einfach auf das Symbol zum Löschen neben der jeweiligen Benutzergruppe oder dem Projekt. Zur dauerhaften Übernahme der vorgenommenen Einstellungen für den Benutzer klicken Sie anschließend auf den Schaltknopf `Speichern`.

{% hint style="warning" %}
Bitte beachten Sie, dass neu hinzugefügte Benutzer, die sich gegen einen konfigurierten LDAP authentifizieren sollen, nach dem Anlegen ein erneutes Mal in der Bearbeitungsmaske geöffnet werden müssen. Erst nach dem Speichern eines Benutzers und dem erneuten Öffnen in der Bearbeitungsmaske ist für den Benutzer das zusätzliche Icon neben der Konfiguration der LDAP-Gruppe sichtbar. Klicken Sie auf dieses Symbol, um die Details des Nutzers neu in den konfigurierten LDAP eintragen zu lassen. Erst nach diesem Schritt ist der Login für diesen Nutzer auch tatsächlich möglich.
{% endhint %}


{% hint style="info" %}
Um einen Nutzer als Super-Administrator festzulegen, muss bereits ein Super-Administrator vorhanden sein, damit dieser weitere Super-Administratoren festlegen kann. Für den Fall, dass kein Super-Administrator bisher gesetzt wurde, muss innerhalb der Datenbank das folgende Kommando abgesetzt werden:

```sql
update benutzer set superadmin = true where BenutzerID=123456;
```
{% endhint %}