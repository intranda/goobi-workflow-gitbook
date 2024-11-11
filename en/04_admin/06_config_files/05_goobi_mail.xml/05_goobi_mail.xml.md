# goobi_mail.xml

The configuration file `goobi_mail.xml` is used to configure mail dispatch for Goobi. The file is usually located here:

```bash
/opt/digiverso/goobi/config/goobi_mail.xml
```

For example, this configuration file looks as follows:

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

| Field | Description |
| :--- | :--- |
| `smtpServer` | SMTP server for mail dispatch |
| `smtpPort` | Port for the SMTP server to use, in case it is not the default port |
| `smtpUser` | Username for authentication on the SMTP server |
| `smtpPassword` | Password for authentication on the SMTP server |
| `smtpUseStartTls` | Activation of the `StartTLS` encryption type |
| `smtpUseSsl` | Activation of the `SSL` encryption type |
| `smtpSenderAddress` | The sender address to be displayed to the recipient. |
| `apiUrl` | URL at which a user can deactivate mail reception |

To deactivate the global sending of emails, it is sufficient to delete the `goobi_mail.xml` file or set the `enabled` attribute to `false`.

Additionally, the content of the emails can be configured. The following keys are available in the `messages files` for this purpose:

| Field | Description |
| :--- | :--- |
| `mail_notification_openTaskSubject` | Subject of the email that is sent when a task is opened. |
| `mail_notification_openTaskBody` | Content of the email that is sent when a task is opened |
| `mail_notification_inWorkTaskSubject` | Subject of the email that is sent when a task is being processed |
| `mail_notification_inWorkTaskBody` | Content of the email that is sent as soon as a task is processed |
| `mail_notification_doneTaskSubject` | Subject of the email that is sent when a task is completed |
| `mail_notification_doneTaskBody` | Content of the email that is sent when a task is completed |
| `mail_notification_errorTaskSubject` | Subject of the email that is sent when a task changes to an error status |
| `mail_notification_errorTaskBody` | Content of the email that is sent when a task changes to an error status |

In addition to normal text or HTML elements, variables can also be used in the `subject` or `body`. The following variables are available for this purpose:

| Variable | Description |
| :--- | :--- |
| `${user}` | Name of the user to whom the e-mail will be sent |
| `${projectname}` | Name of the project to which the task belongs |
| `${processtitle}` | Name of the operation to which the task belongs |
| `${stepname}` | Name of the current task |
| `${url_cancelStep}` | URL to unsubscribe from notifications for this type of task |
| `${url_cancelProject}` | URL to unsubscribe notifications for all tasks of the project |
| `${url_cancelAll}` | URL to unsubscribe from all notifications |

For example, an email text could be configured as follows:

{% code title="messages_de.properties" %}
```ini
mail_notification_openTaskBody=<html><body><h3>Hallo ${user},</h3><br /><p>folgender Schritt wurde ge\u00F6ffnet und kann nun bearbeitet werden:<ul><li>Projekt: ${projectname}</li><li>Vorgang: ${processtitle}</li><li>Schritt: ${stepname}</li></ul></p><div><a href="${url_cancelStep}">Benachrichtigungen f\u00FCr Schritte mit diesem Namen abbgestellen</a><a href="${url_cancelProject}"></div><div>Benachrichtigungen f\u00FCr dieses Projekt abbestellen</a></div><div><a href="${url_cancelAll}">Alle Benachrichtigungen abbestellen</a></div></body></html>
```
{% endcode %}