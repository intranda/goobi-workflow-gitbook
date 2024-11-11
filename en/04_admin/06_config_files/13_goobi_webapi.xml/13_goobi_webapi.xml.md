# goobi_webapi.xml

The `goobi_webapi.xml` configuration file is used to enable certain API endpoints of the Goobi Workflow Server for other servers or clients. The file is usually located at the following location:

```bash
/opt/digiverso/goobi/config/goobi_webapi.xml
```

For example, this configuration file looks as follows:

{% code title="goobi_webapi.xml" %}
```xml
<?xml version="1.0"?>
<config_webapi>
  <credentials ip="0:0:0:0:0:0:0:1" password="CHANGEME">
    <command name="closeStep"/>
    <command name="addToProcessLog"/>
    <command name="setErrorStep"/>
    <command name="help"/>
  </credentials>
  <credentials ip="127.0.0.1" password="CHANGEME">
    <command name="closeStep"/>
    <command name="addToProcessLog"/>
    <command name="setErrorStep"/>
    <command name="help"/>
  </credentials>
  <credentials ip="10.20.30.40" password="super_admin_password">
    <command name="/"/>
  </credentials>
  <credentials ip="20.40.60.80" password="admin_password">
    <command name="/process"/>
  </credentials>
  <credentials ip="40.60.80.100" password="user_password">
    <command name="/process/check"/>
  </credentials>
</config_webapi>
```
{% endcode %}

Goobi Workflow provides a REST API for communicating between the Goobi Workflow Server and other network participants using HTTPS protocol and JSON data objects.

The functions that are performed using the API are specified as endpoints in the URL. For example, the following URL returns the details of a process with the specified ID `MY_ID`:

```text
http://goobi.your-domain.org/Goobi/api/process/details/id/MY_ID?token=test
```

However, there are also commands like `process/create` or `process/delete` that may only be executed by certain users.

A `user` can be another server or client. In both cases it needs a fixed IP address for which access is granted.

For each access right a `<credentials>` element is used. The `ip` parameter contains either the IPv4 address or the IPv6 address of the user. The `password` parameter specifies a token that must be specified as a URL parameter in a request from the respective user IP address. For example, if the `password="super_user_password"` token is specified in the access rule for the `ip="10.20.30.40"` IP address, an API request can only be answered if the user with the `10.20.30.40` IPv4 address uses the `token=super_user_password` URL parameter.

The token should not contain any special characters or URL syntax characters. Otherwise, these must be encoded later in the request according to the URL specification. If the `My Password` token is specified in the access rule, the space character in the request URL must be replaced with the hexadecimal value `0x20` and the URL parameter looks like this: `token=My%20Password`.


{% hint style="info" %}
**Note:** Since Goobi uses the HTTPS protocol, the request is transmitted encrypted and the token cannot be read by third parties.
{% endhint %}

Each access rule contains one or more API commands. These commands or groups of commands can be used as soon as the combination of IP address and token described above matches. A command is defined with the `<command>` element and has exactly one `name` parameter containing the command. The command itself can optionally start with a slash (`/`).

In the above example, three access rules are specified that define the different access rights for different user groups. Thus, a super administrator has the ability to use all API commands (`/`). A normal administrator can execute all subcommands of `process`. For a standard user, only the `process/check` command is enabled.