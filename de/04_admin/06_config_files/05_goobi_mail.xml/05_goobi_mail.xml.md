# goobi_mail.xml

In der Konfigurationsdatei `goobi_mail.xml` wird der E-Mail-Versand für Goobi konfiguriert. Die Datei befindet sich üblicherweise hier:

```bash
/opt/digiverso/goobi/config/goobi_mail.xml
```

Beispielhaft sieht diese Konfigurationsdatei wie folgt aus:

{% code title="goobi_mail.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<goobiMail>
    <configuration enabled="true">
        <smtpServer>mail.example.com</smtpServer>
        <smtpPort>5587</smtpPort>
        <smtpUser>do-not-reply@example.com</smtpUser>
        <smtpPassword>PASSWORD</smtpPassword>
        <smtpUseStartTls>false</smtpUseStartTls>
        <smtpUseSsl>true</smtpUseSsl>
        <smtpSenderAddress>do-not-reply@example.com</smtpSenderAddress>
    </configuration>
    <apiUrl>http://example.com/goobi/api/mails/disable</apiUrl>
</goobiMail>
```
{% endcode %}

| Feld                | Beschreibung                                                   |
| ------------------- | -------------------------------------------------------------- |
| `smtpServer`        | SMTP Server für den Mailversand                                |
| `smtpPort`          | Port für den SMTP Server, wenn dieser von dem Standardport abweicht |
| `smtpUser`          | Benutzername zur Authentifizierung an dem SMTP Server          |
| `smtpPassword`      | Passwort zur Authentifizierung an dem SMTP Server              |
| `smtpUseStartTls`   | Aktivierung der Verschlüsselungsart `StartTLS`                 |
| `smtpUseSsl`        | Aktivierung der Verschlüsselungsart `SSL`                      |
| `smtpSenderAddress` | Die Absenderadresse, die dem Empfänger angezeigt werden soll   |
| `apiUrl`            | URL, unter der ein Nutzer den E-Mail-Empfang deaktivieren kann |

Um den E-Mail-Versand global zu deaktivieren, reicht es aus, die Datei `goobi_mail.xml` zu löschen oder das Attribut `enabled` auf den Wert `false` zu setzen.

Zusätzlich kann noch der Inhalt der E-Mails konfiguriert werden. Dazu stehen in den `messages-Dateien` folgende Schlüssel zur Verfügung:

| Feld                                  | Beschreibung                                                                             |
| ------------------------------------- | ---------------------------------------------------------------------------------------- |
| `mail_notification_openTaskSubject`   | Betreff der E-Mail, die beim Öffnen eine Aufgabe versendet wird                          |
| `mail_notification_openTaskBody`      | Inhalt der E-Mail, die beim Öffnen einer Aufgabe versendet wird                          |
| `mail_notification_inWorkTaskSubject` | Betreff der E-Mail, die versendet wird, sobald eine Aufgabe bearbeitet wird              |
| `mail_notification_inWorkTaskBody`    | Inhalt der E-Mail, die versendet wird, sobald eine Aufgabe bearbeitet wird               |
| `mail_notification_doneTaskSubject`   | Betreff der E-Mail, die beim Abschliessen einer Aufgabe versendet wird                   |
| `mail_notification_doneTaskBody`      | Inhalt der E-Mail, die beim Abschliessen einer Aufgabe versendet wird                    |
| `mail_notification_errorTaskSubject`  | Betreff der E-Mail, die versendet wird, wenn eine Aufgabe in einen Fehlerstatus wechselt |
| `mail_notification_errorTaskBody`     | Inhalt der E-Mail, die versendet wird, wenn eine Aufgabe in einen Fehlerstatus wechselt  |

Neben normalen Text oder HTML-Elementen können im `subject` oder `body` auch Variablen genutzt werden. Folgende Variablen stehen hierfür zur Verfügung:

| Variable               | Beschreibung                                                                |
| ---------------------- | --------------------------------------------------------------------------- |
| `${user}`              | Name des Nutzers, an den die E-Mail versendet wird                          |
| `${projectname}`       | Name des Projekts, zu dem die Aufgabe gehört                                |
| `${processtitle}`      | Name des Vorgangs, zu dem die Aufgabe gehört                                |
| `${stepname}`          | Name der aktuellen Aufgabe                                                  |
| `${url_cancelStep}`    | URL zur Abbestellung der Benachrichtigungen für diese Art von Aufgaben      |
| `${url_cancelProject}` | URL zur Abbestellung der Benachrichtigungen für alle Aufgaben des Projektes |
| `${url_cancelAll}`     | URL zur Abbestellung aller Benachrichtigungen                               |

Ein E-Mail-Text könnte zum Beispiel wie folgt konfiguriert werden:

{% code title="messages_de.properties" %}
```ini
mail_notification_openTaskBody=<html><body><h3>Hallo ${user},</h3><br /><p>folgender Schritt wurde ge\u00F6ffnet und kann nun bearbeitet werden:<ul><li>Projekt: ${projectname}</li><li>Vorgang: ${processtitle}</li><li>Schritt: ${stepname}</li></ul></p><div><a href="${url_cancelStep}">Benachrichtigungen f\u00FCr Schritte mit diesem Namen abbgestellen</a><a href="${url_cancelProject}"></div><div>Benachrichtigungen f\u00FCr dieses Projekt abbestellen</a></div><div><a href="${url_cancelAll}">Alle Benachrichtigungen abbestellen</a></div></body></html>
```
{% endcode %}