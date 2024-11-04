# User authentication using LDAP

## General

Goobi usually uses an LDAP server to authenticate users. This makes it possible to connect to the provided network drive with the same user name and password as in Goobi. In the configuration file `goobi_config.properties` it is specified on the one hand whether LDAP is to be used in principle by Goobi, on the other hand the truststore used is also configured there. All other settings for LDAP connections and user groups are made in the administration area of the user interface.

The LDAP server needs to include the following schemas: `COSINE`, `inetOrgPerson`, `NIS` und `SAMBA`..

## Configuration in the file goobi\_config.properties

In the file `goobi_config.properties` the following settings for LDAP and the truststore are available:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `ldap_use` | Boolean | `false` | This value indicates whether an LDAP service should be used. |
| `truststore` | Text | | This value specifies where the truststore is located. |
| `truststore_password` | Text | | This value specifies the password for authentication in the truststore. |

**Note:** In previous Goobi versions there were `ldap_keystore` and `ldap_keystore_password` settings at this point. These have been renamed because the keystore can be used for other purposes as well. These settings are **no longer supported**.

**Note:** Occasionally, the incorrectly passed `ldap_truststore` and `ldap_truststore_password` settings appear in older configuration files. These settings do not exist in Goobi and are accordingly **not supported**.

The configuration within the `goobi_config.properties` configuration file when using a local LDAP server may look like the following, for example:

```text
# -----------------------------------
# ldap
# -----------------------------------

# Use LDAP server for authentication
ldap_use=true

# -----------------------------------
# truststore
# -----------------------------------

# Keystore for LDAP and other services
# There is no default value, but the truststore can look like this example:
# /opt/digiverso/goobi/scripts/mykeystore.ks
#truststore=
#truststore_password=
```

## Configuration in Goobi

<!---
Dieses Bildschirmfoto ist veraltet und kann durch die anderen vier Bilder (siehe Kommentare unten) ersetzt werden.
Es fehlen auf diesem Bild zwei neuere Einstellungen und ein paar Details entsprechen nicht mehr der heutigen Ansicht.
![Configuration of LDAP groups](../../.gitbook/assets/30-60e.png)
-->

LDAP groups can be set up in Goobi in the 'Administration' -> 'Authentication' section. A list of authentication options that have already been set up is displayed first. To set up an LDAP group, a new authentication must be created.

<!--- Hier soll ein Bild von ldap_all.xhtml mit drei Beispiel-Authentifikationen (OpenID, LDAP und Datenbank) zu sehen sein. -->
![List of already set up authentifications](PLACEHOLDER.png)

Currently, three authentication types are available. For all of them at least a name, a type and a login shell command must be selected. If LDAP is selected as type, some more options are available. There are also a total of three tabs available for LDAP (`General`, `Details` and `Authentication`).

On the `General` page, basic settings for the LDAP group are made, such as the URL of the LDAP server, the User DN (distinguishing name) and Samba IDs. The `User DN` field is used for mapping from the user identification in the Goobi database to the user identification in the LDAP group. The placeholder `{login}` represents the login name of a user and must be specified so that Goobi can later create a named LDAP account for each new Goobi account.

| Property | Description |
| -------- | ----------- |
| Name | A name for the authentication type is specified here. This should be unique within Goobi. |
| Type | This menu can be used to select what type of authentication it is. The options 'Database' and 'OpenID' can be used without detailed configuration. If LDAP is selected, further setting options appear below. |
| LDAP URL | The URL of the LDAP service is specified here. The URL must also contain the correct port number. If the LDAP server runs on the same machine, `localhost:389` can be specified here. |
| LDAP User DN | This field contains information for creating LDAP accounts based on Goobi database accounts. The `{login}` placeholder must be used so that Goobi can use the correct user name later. |
| Samba SID | This is the user identification for the associated Samba server. |
| Login Shell | Here you can specify a bash script to be executed when a user logs in. |
| Samba Primary Group SID | The group ID for the user group at the Samba server is specified here. |

<!--- Hier soll ein Bild von ldap_edit.xhtml, Tab 1 (Allgemein) zu sehen sein. -->
![Configuration of an LDAP group: General](PLACEHOLDER.png)

On the page `Details`, many more details are configured for the LDAP group.

| Property | Description |
| -------- | ----------- |
| User directory | The directory for user accounts is specified here. The placeholder `{login}` is used here so that Goobi can use the correct user name later. |
| GID number | The group ID number for the LDAP group is specified here. If multiple LDAP groups are set up, these IDs must be different. |
| Object classes | Additional parameters for the LDAP group can be specified in this field. These are listed comma separated. |
| LDAP SN | In this field the serial number of the user on the LDAP system is specified. The placeholder `{login}` can also be used for this. |
| LDAP UID | This field specifies the user ID to be used for the respective LDAP account. Here, too, `{login}` can be used as a placeholder. |
| Description | This description will be added to the users created by Goobi in the LDAP system. |
| Display name | This text field contains a placeholder for the user's full displayed name. Here `{user full name}` can be used. This will display first name and last name later. |
| Geocs | This field can be used to specify additional information about Goobi users in the LDAP group, such as a location or contact details. |
| Samba Account Flags | This field is used to specify additional parameters for the Samba account. |
| Samba Logon Script | This field can be used to specify a script file to be executed when a user logs on to the Samba system. To allow a separate script file for each user, the placeholder `{login}` can be used here as well. |
| Password change required by Samba | Here you can specify a time period after which each user has to change his password for security reasons. Since this password is also the Goobi password of the corresponding user, a user has to change his Goobi password to change the Samba password as well. |
| Samba Password History | Here you can specify details about the storage of the last used passwords of a Samba user. |
| Samba Logon Hours | Here a time period in binary format (in hours) can be specified when a user can logon to the Samba system. To always allow this, the value must contain 21x 'F'. |
| Samba Kickoff Time | Here you can specify the time in milliseconds after which a user is automatically logged off the Samba system. |
| Use user directory from the configuration file | This field can be set to not let LDAP determine the user directory, but to use the one specified above. |
| Attribute name user directory | This value can be used on older systems to specify which key is used in the Goobi configuration to specify the LDAP user home directory. |

<!--- Hier soll ein Bild von ldap_edit.xhtml, Tab 2 (Details) zu sehen sein. -->
![Configuration of an LDAP group: Details](PLACEHOLDER.png)

The `Authentication` page specifies technical details for authentication to the LDAP service set up in the `General` tab. This page contains some settings that previously could only be made once in the `goobi_config.properties` configuration file and can now be specified for this particular LDAP authentication.

| Property | Description |
| -------- | ----------- |
| Administrator account name | The user name of the administrator account at the LDAP service is specified here. Additional parameters (separated by commas) are specified to identify the administrator. |
| Administrator password | The password for the administrator account at the LDAP service is specified here. |
| LDAP next free unix id | A placeholder for the next free user ID on the LDAP server is specified in this field. In addition, further parameters for user identification are specified (separated by commas). |
| Root certificate | The SSL certificate for the connection to the LDAP server is specified here. |
| PDC certificate | The PDC certificate for the connection to the LDAP server is specified here. |
| Encryption type | The encryption type for connections with the LDAP service can be selected here. Currently `SHA` and `MD5` are available. |
| SSL | This option can be selected to use Secure Sockets Layer (SSL) encryption. **Note:** SSL encryption is deprecated and it is recommended to use TLS encryption. |
| Read only access | This option can be selected if users should have read-only access to the LDAP system. |
| Access without authentication | This option can be used to set whether anonymous access to the LDAP system is allowed. |
| TLS | This option can be selected to use Transport Layer Security (TLS) encryption. | 

<!--- Hier soll ein Bild von ldap_edit.xhtml, Tab 3 (Authentifizierung) zu sehen sein. -->
![Configuration of an LDAP group: Authentication](PLACEHOLDER.png)

## Configuration in the operating system

As well as these Goobi-specific settings, it is important to ensure that LDAP users are identified to the operating system. The LDAP information must be entered correctly. This is particularly important for the following files:

```bash
/etc/ldap/ldap.conf
/etc/ldap.conf
/etc/nsswitch.conf
/etc/pam.d/*
```

The use of the LDAP server must be enabled for SAMBA. Since Ubuntu 14.04 LTS this is set by default.