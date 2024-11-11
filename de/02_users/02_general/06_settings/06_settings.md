# Eigene Einstellungen

Wenn Sie in Goobi eingeloggt sind, haben Sie die Möglichkeit, Einstellungen für Ihr eigenes Nutzerprofil festzulegen. Diese Einstellung erreichen Sie indem Sie in der Menüleiste auf Ihren Nutzernamen und dann den Menüpunkt Benutzerkonfiguration anklicken. In dem nun geöffneten Formular haben Sie die Möglichkeit, Details für Ihr persönliches Profil festzulegen.

![Benutzerkonfiguration - Übersicht](screen1_de.png)

![Benutzerkonfiguration - Metadateneditor](screen2_de.png)


In dem Bereich der `Allgemein` lassen sich einige Werte für die Arbeit mit Goobi festlegen. Der Wert für die `Zeitüberschreitung der Session` legt hier in Minuten fest, nach welcher Zeit, in der durch Sie nicht in Goobi gearbeitet wurde, Sie automatisch von Goobi abgemeldet werden. Ein automatisches Ausloggen findet wie im Beispiel dieser Abbildung nach 120 Minuten Inaktivität durch Goobi statt.

Der Wert der `Tabellengröße` (in diesem Beispiel: 10) legt fest, wie viele Zeilen die Tabellen in Goobi auf einer Seite auflisten sollen, bevor für die Einsicht auf weitere Daten auf die nächste Tabellenseite geblättert werden muss.

![Benutzerkonfiguration - Vorgänge](screen3_de.png)

Die `Sprache der Metadaten` legt fest, welche Sprache des konfigurierten Regelsatzes für die Struktur- und Metadaten innerhalb des eingebetteten METS-Editors in Goobi verwendet werden soll. Der hier festgelegte Wert muss dabei nicht identisch mit Ihrer konfigurierten Sprache sein, die für die Goobi-Oberfläche gewählt wurde. Die hier definierte Sprache muss jedoch im Regelsatz konfiguriert sein. Mittels dieser Einstellung ist es möglich, dass z. B. besondere Sprachen für Struktur- und Metadaten vorgegeben werden können, unabhängig von den Sprachen, in denen Goobi selbst verfügbar ist.

Mit der Checkbox `Vorgangsdatum anzeigen` kann der Benutzer festlegen, dass ihm im Bereich Meine Aufgaben und auch im Bereich der `Vorgänge` und `Produktionsvorlagen` eine zusätzliche Spalte mit dem Datum angezeigt wird, an dem der entsprechende Vorgang angelegt wurde.

![Benutzerkonfiguration - Aufgaben inklusive aktivierter Hilfefunktion](screen4_de.png)

Im Bereich `E-Mail Benachrichtigungen` lässt sich konfigurieren, welche E-Mails man bei Statusänderungen in Goobi erhalten möchte. Dazu wird zunächst die Sprache festgelegt, in der die E-Mails verfasst sind. Unterhalb der Sprachauswahl werden die Projekte aufgelistet, in denen der Benutzer Mitglied ist. Sobald auf eines der Projekte geklickt wurde, wird dieses aufgeklappt und die Liste der Aufgaben aufgelistet, die für die Nutzergruppen freigeschaltet sind, in denen der Nutzer Mitglied ist.

Hier lassen sich nun diejenigen Aufgaben auswählen, über die der Nutzer im Falle der ausgewählten Statusänderung informiert werden möchte. Dies ist für einzelne Aufgaben ebenso möglich wie auch für sämtliche Aufgaben.

{% hint style="info" %}
Um die Mail-Benachrichtigungen zu aktivieren und mit allen Funktionalitäten nutzen zu können, müssen eventuell noch Änderungen an der Goobi-Konfiguration vorgenommen werden:

1. Die Konfigurationsdatei {% page-ref page="../../../04_admin/06_config_files/05_goobi_mail.xml/05_goobi_mail.xml.md" %} anlegen und anpassen
2. Ein `jwtSecret` in der Datei {% page-ref page="../../../04_admin/06_config_files/02_goobi_config.properties/02_goobi_config.properties.md" %} setzen
3. Den Mail-Deaktivierungs-Endpoint in der  Datei {% page-ref page="../../../04_admin/06_config_files/12_goobi_rest.xml/12_goobi_rest.xml.md" %} freischalten
{% endhint %}

Verfügt der Nutzer über das Benutzerrecht `Benachrichtigungen bei allen Statusänderungen`, werden sämtliche Aufgaben angezeigt statt nur derjenigen, in denen man selbst Mitglied ist. Darüber hinaus lassen sich in diesem Falle auch Benachrichtigungen für weitere Statusänderungen auswählen, wie z.B. für Fehlerfälle oder den Abschluss der Bearbeitung.

Zu den Werten, die innerhalb der Benutzerkonfiguration vorgenommen werden können, erhalten Sie eine ausführliche Erläuterung, indem sie innerhalb der Menüleiste einfach die Hilfefunktion aktivieren. Anschliessend werden Beschreibungen zu den einzelnen Feldern angezeigt, die Ihnen bei der Eingabe Unterstützung geben.

Bitte beachten Sie, dass erst ein Klick auf `Speichern` die hier eingestellten Werte übernimmt.