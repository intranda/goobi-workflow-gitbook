# goobi_config.properties

In the configuration file `goobi_config.properties`, some fundamental settings are done for Goobi Workflow. The file is usually located at the following file system path:

```bash
/opt/digiverso/goobi/config/goobi_config.properties
```

For example, this configuration file looks as follows:

{% code title="goobi_config.properties" %}
```ini
# -----------------------------------
# application information
# -----------------------------------

ApplicationTitle=http://goobi.io
ApplicationHeaderTitle=Goobi workflow

# Text that describes the website
ApplicationHomepageMsg=info
ApplicationWebsiteMsg=info

# Developer mode (true) or production mode (false)
developing=false

# -----------------------------------
# directories
# -----------------------------------

# Main folder for Goobi incl. subfolders config, xslt, rulesets, metadata etc.
# Path configured here should end with path separator
# sample and default if missing: /opt/digiverso/goobi/
goobiFolder=/opt/digiverso/goobi/

# use this folder if metadata directory is not goobiFolder + metadata/
#dataFolder=

# parent folder for home directories, default is goobiFolder + users/
#dir_Users=/home/

#folder for debugging files, can be used by opac beautifier 
#debugFolder=

# folder for the process log
# for compatibility reasons, also folder_processlog_internal is requested
#folder_journal_internal=intern

# folder for mass upload functionality
#doneDirectoryName=fertig/

# path for swapping, this could for example be /tmp/unused/
#swapPath=

# naming rule for master folder 
#process.folder.images.master={processtitle}_master

# naming rule for media folder
#process.folder.images.main={processtitle}_media

# naming rule for source folder
#process.folder.images.source={processtitle}_source

# naming rule for image fallback folder - not needed any more, is replaced with thumbs directories
# default value is an empty string
#process.folder.images.fallback={processtitle}_jpeg

# naming rule for ocr text folder
#process.folder.ocr.txt={processtitle}_txt

# naming rule for pdf folder
#process.folder.ocr.pdf={processtitle}_pdf

# naming rule for ocr xml folder
#process.folder.ocr.xml={processtitle}_xml

# naming rule for ocr alto folder
#process.folder.ocr.alto={processtitle}_alto

# naming rule for import folder
#process.folder.import=import

# naming rule for export folder
#process.folder.export=export

# create master directory if it does not exist
createOrigFolderIfNotExists=true

# indicates whether the source folder should be created automaticly or not, default is false
createSourceFolder=false

# -----------------------------------
# global user settings
# -----------------------------------

# set a default language, language can be changed by the user. If no language is set, the browser default is used
#defaultLanguage=

# anonymized statistics, displaying user on steps, etc
# possible values: true/false
anonymize=false

# enable or disable usage of gravatar icons
#enableGravatar=true

# The minimum password length for user accounts
# This value is also used for new generated passwords, they are generated with
# this length + 10
minimumPasswordLength=8

# Multiple additional user rights can be set here, default is an empty list
userRight=

# -----------------------------------
# user interface features
# -----------------------------------

ui_useIntrandaUI=true

# include the file accessibility.css in the template. Can be overwritten in user settings
renderAccessibilityCss=false

# show statistics box on startpage, default is true
showStatisticsOnStartPage=true

# enable or disable the finalize button in task/batch edition screens. The default value is to display the button
#TaskEnableFinalizeButton=true

#show button to link into home directory
#ui_showFolderLinkingInProcessList=false

#display confirmation dialogue when link into home directory is set from process list 
#confirmLinking=false

# A button to reimport already exported content can be activated
#renderReimport=false

# use this parameter to exlude user agents from session list
excludeMonitoringAgentName=Munin
excludeMonitoringAgentName=munin
excludeMonitoringAgentName=nagios-plugins
excludeMonitoringAgentName=monitoring-plugins
excludeMonitoringAgentName=ELB-HealthChecker/2.0
excludeMonitoringAgentName=python-requests

# -----------------------------------
# ldap
# -----------------------------------

# Logins ueber LDAP verwenden
ldap_use=false

# -----------------------------------
# truststore
# -----------------------------------

# Keystore for LDAP and other services
# There is no default value, but it can look like this example:
# /opt/digiverso/goobi/scripts/mykeystore.ks
#truststore=
#truststore_password=

# -----------------------------------
# open id connect
# -----------------------------------

# Must be set to true to use OpenID Connect
#useOpenIdConnect=false
# Automatic redirection to OpenID Connect login
#OIDCAutoRedirect=false
# The OpenID Connect authentication server
#OIDCAuthEndpoint=
# API endpoint for logout command
#OIDCLogoutEndpoint=
# The issuer of OpenID Connect
#OIDCIssuer=
# The JWK set of OpenID Connect
#OIDCJWKSet=
# The client ID of this server
#OIDCClientID=
# The notifying method
#OIDCIdClaim=email
# Can be set to true to use SSO logout
#useOIDCSSOLogout=false

# -----------------------------------
# single sign on
# -----------------------------------

# Enables a login method via HTTP header field
#EnableHeaderLogin=false
# The login type via the HTTP header field
#SsoParameterType=header
# The name of the HTTP header field to login
#SsoHeaderName=Casauthn
# Enables a logout page for 
#showSSOLogoutPage=false

# -----------------------------------
# external users
# -----------------------------------

# enable an additional login area for external users, it allows a different UI and a self registration 
#EnableExternalUserLogin=false

# assign the self registered users to this institution, this could be "goobi" for example
#ExternalUserDefaultInstitution=

# assign the self registered users to this authentication type
#ExternalUserDefaultAuthentication=

# -----------------------------------
# database search
# -----------------------------------

# enable fulltext search mode for metadata searches. Doesn't work on h2 or older mysql/mariadb databases
useFulltextSearch=false

# configure fulltext search mode, possible values are 'NATURAL LANGUAGE MODE' or 'BOOLEAN MODE'
# see https://www.w3resource.com/mysql/mysql-full-text-search-functions.php
#FulltextSearchMode=BOOLEAN MODE

#truncation characters in sql queries
#DatabaseLeftTruncationCharacter=%
#DatabaseRightTruncationCharacter=%

# enable this to use a specific index for my tasks queries. The best table index might be different from database to database
# if commented out, no specific index is used
#SqlTasksIndexname=status_x_title

#generate one metadata index field for multiple metadata coming from the METS file
#index.ids=CatalogIDDigital,CatalogIDSource

# -----------------------------------
# processes and process log
# -----------------------------------

# Set this to true to automatically reset the process log if processes are cloned
#ProcessCreationResetJournal=false

# allow white spaces in directory names or replace them with __
#dir_allowWhiteSpaces=false

# allow import with plugin mechanism for mass imports
massImportAllowed=false

# allow process title duplication
#MassImportUniqueTitle=true

# number of maximal items per batch, if not configured the default is 100
batchMaxSize=500

# enables the option to see the last edition date, username and title of the last finished step
ProcesslistShowEditionData=false

# Defines the start times of the daily delay job, the daily vocab job and the daily history analyser job
# If missing or value is -1, the job is disabled.
# Every other number is interpreted as MILLISECONDS after midnight.
# These values are requested by org.goobi.production.flow.jobs.JobManager
dailyDelayJob=-1
dailyVocabJob=-1
dailyHistoryAnalyser=-1

# This is the upload frequency of the goobi authentication server in MINUTES
# This value is requested by org.goobi.production.flow.jobs.JobManager
goobiAuthorityServerUploadFrequencyInMinutes=-1

# Activates additional columns for search result
downloadAvailableColumn=CatalogIdDigital
downloadAvailableColumn=TitleDocMain
downloadAvailableColumn=PublicationYear
downloadAvailableColumn=PlaceOfPublication

# Text templates for error reporting and problem solutions
#task.error.Missing\ pages=The following pages are missing: {}
#task.error.Blurred\ images=The images {} are unsharp. Please create these again.
#task.solution.Problem\ solved=The problem was solved. {}
#task.solution.The\ original\ print\ is\ blurred=The original pages are printed blurry. It is not possible to create sharper images. {}

# -----------------------------------
# scripts
# -----------------------------------

# These values can be set to paths to bash script files that do the concerning tasks
#script_createDirUserHome=
#script_createDirMeta=
#script_createSymLink=
#script_deleteSymLink=

# -----------------------------------
# s3 bucket
# -----------------------------------

# Can be set to true to enable S3 usage
#useS3=false

# Can be set to true to use a custom S3 service
#useCustomS3=false

# If useCustomS3 is enabled, the endpoint can be specified here
#S3Endpoint=

# The used S3 bucket is specified here
#S3bucket=

# The access id of the account of goobi against the S3 service
#S3AccessKeyID=

# The secret access key of that account
#S3SecretAccessKey=

# The number of retries if a connection does not succeed
#S3ConnectionRetry=10

# The timeout for any connection tries
#S3ConnectionTimeout=10000

# The timeout for socket concerning things
#S3SocketTimeout=10000

# -----------------------------------
# proxy server
# -----------------------------------

http_proxyEnabled=false
#http_proxyUrl=127.0.0.1
#http_proxyPort=3128
http_proxyIgnoreHost=127.0.0.1
http_proxyIgnoreHost=localhost

# -----------------------------------
# internal servers and interfaces
# -----------------------------------

# allow external programms to send commands to Goobi via WebAPI
useWebApi=false

# The token salt value can be used to make authentication on the Goobi REST API more secure
#apiTokenSalt=

#the jwtSecret is needed to (among others) authenticate mail delivery deactivation
#jwtSecret=

# goobi base url, can be used when url cannot be detected from user sessions
goobiUrl=http://localhost:8080/goobi

#The url of the plugin server of goobi
#pluginServerUrl=

# Basispfad fuer OCR (ohne Parameter)
ocrUrl=

# TimeOut for GoobiContentServlet-Request via HTTP in ms (default value, if nothing defined here: 60000)
goobiContentServerTimeOut=30000

# The url, the user name, the password and the upload frequency can be set
# for the content server here
goobiAuthorityServerUrl=
goobiAuthorityServerUser=
goobiAuthorityServerPassword=
goobiAuthorityServerUploadFrequency=

# account name for geonames api
#geonames_account=

# -----------------------------------
# message broker
# -----------------------------------

# Set this to true to let the message broker start
#MessageBrokerStart=false

# The default value is the configuration folder + "goobi_activemq.xml"
#ActiveMQConfig=

# The server IP or domain of the message broker
#MessageBrokerServer=localhost

# The port number of the message broker
#MessageBrokerPort=61616

# The password to access the message broker
#MessageBrokerPassword=

# The number of parallel messages can be set here
#MessageBrokerNumberOfParallelMessages=1

# External Queues can be enabled here
allowExternalQueue=false

# The type of the external queue, currently the possible values are "SQS" and "activeMQ"
externalQueueType=activeMQ

#set this to true if you want to test the SQS external queue with elasticMQ
useLocalSQS=false

# -----------------------------------
# mets editor
## mets editor / general properties
# -----------------------------------

# initialise all sub elements in Mets editor to assign default values, default value is true
MetsEditorEnableDefaultInitialisation=true

# create pagination when mets editor is opened 
#MetsEditorEnableImageAssignment=true

# use special pagination type for automatic default pagination (uncounted, roman, arabic)
MetsEditorDefaultPagination=uncounted

# configure the locking time for mets editor timeout in ms, default is 30 minutes
MetsEditorLockingTime=1800000

# use external ocr for text in mets editor or use existing files 
#MetsEditorUseExternalOCR=false

# The number of backups can be set here. 0 means that no backups are created
numberOfMetaBackups=0

# -----------------------------------
## mets editor / user interface
# -----------------------------------

# OCR-Button fuer ausgewaehltes Strukturelement anzeigen
showOcrButton=false

# Display the METS editor area for manipulation of the image set
MetsEditorDisplayFileManipulation=false

# Display archived folders
MetsEditorShowArchivedFolder=false

# display/hide metadata popup in structure tree
#MetsEditorShowMetadataPopup=true

# use a maximum of characters to display titles in the left part of mets editor, the default value is 0 (everything is displayed)  
MetsEditorMaxTitleLength=0

# -----------------------------------
## mets editor / images and thumbnails
# -----------------------------------

# enable to show image comments in METS editor, imageQA and LayoutWizzard
ShowImageComments=false

# Number of images in thumbnail view
MetsEditorNumberOfImagesPerPage=96

# This value can be set to true to use image tiling in the METS editor
MetsEditorUseImageTiles=true

# sorting of images
# At this time implemented sorting options:
# number (default): 1 is lesser then 002, compares the number of image names, characters other than digits are not supported
# alphanumeric: 1 is greater then 002, compares character by character of image names, all characters are supported
ImageSorting=number

# Prefix for image names as regex. Default is 8 digits \\d{8} and gets validated
ImagePrefix=\\w+
#ImagePrefix=\\d{8}
#ImagePrefix=.+

# define owner of images, when read access is provided. Default is root user 
#UserForImageReading=root

# This can be set to true to use image thumbnails
UseImageThumbnails=true

# Size of thumbnails in METS editor
MetsEditorThumbnailsize=200

# Maximum number of requested thumbnails to not overload the server
MaxParallelThumbnailRequests=100

# The maximum image size in pixels
MetsEditorMaxImageSize=15000

# The maximum image size in bytes, MaxImageFileSizeUnit must be set as factor
MaxImageFileSize=4000

# The unit for the maximum image size in bytes, MaxImageFileSize must be set as numeric value
MaxImageFileSizeUnit=MB

# Sizes for big images in METS editor to allow standard display and deep zoom
# This value can be set multiple times
MetsEditorImageSize=

# The size of image tiles
# This value can be set multiple times
MetsEditorImageTileSize=

# The scale of image tiles
# This value can be set multiple times
MetsEditorImageTileScale=

# A list of image file types that are used for process checks
historyImageSuffix=.tif

# -----------------------------------
## mets editor / validation
# -----------------------------------

# grundsaetzliche Metadatenvalidierung durchfuehren oder nicht
useMetadatenvalidierung=true

# Validate the images in the METS editor
MetsEditorValidateImages=true

# regular expression to check if the process title is valid
validateProcessTitelRegex=[\\w-]*

# regular expression for all characters to remove in title generation
ProcessTitleGenerationRegex=[^\\w-]

# -----------------------------------
## mets editor / export
# -----------------------------------

# The path to the exif tool to export the images
ExportExiftoolPath=/usr/bin/exiftool

# set if Master-Images-Folder 'orig_' should be used at all
useOrigFolder=true

# if this parameter is missing or 'false' the old export mechanism is used, otherwise there is no timelimit for export 
exportWithoutTimeLimit=true

# Validate images on mets export. Default value is true
ExportValidateImages=true

# Defines the name of the metadata field where the project title gets exported.
# If the field is empty, missing or contains an unknown value, the project title is not written.
#ExportMetadataForProject=MetadataName

# Defines the name of the metadata field where the institution name gets exported.
# If the field is empty, missing or contains an unknown value, the institution name is not written.
#ExportMetadataForInstitution=MetadataName

# Defines the name of the metadata field where the dfg viewer link gets exported.
# If the field is empty, missing or contains an unknown value, the link is not written.
#ExportMetadataForDfgViewerUrl=MetadataName

# Define if files shall get exported if optional file groups for these files are configured
ExportFilesFromOptionalMetsFileGroups=false

# export in temporary file, move it to destination or export directly to destination
ExportInTemporaryFile=false

# Use UUID for each file id instead of incremental numbers
ExportCreateUUID=true

# Create premis elements for technical metadata for each exorted file  
ExportCreateTechnicalMetadata=false

# Define here if in the automatic export images shall be exported too or not
automaticExportWithImages=true

# Define here if in the automatic export OCR results shall be exported too or not
automaticExportWithOcr=true

# Allow the PDF generation as downloadable file instead of storing it into the users home directory
pdfAsDownload=true
```
{% endcode %}

## General

This configuration file has been used in Goobi Workflow for a very long time and therefore contains partly obsolete settings which are supported nowadays only for compatibility reasons. These are marked separately and if necessary describe an alternative how to replace these settings.

Since the settings have been added over a long period of time and are still being added, different naming conventions have always been used in the variable names. Therefore, special attention must be paid to the correct use of upper and lower case as well as underscores and periods in the variable names.

This configuration file contains settings for many different topics. Sometimes it is unavoidable that certain settings fit to several topics and, depending on the application purpose, can also be in different categories. If certain settings cannot be found at the expected place, it is recommended to search the page with the search function of the browser (usually Ctrl+F).

Many settings have default values that are chosen to be useful for most users. Therefore, not all settings need to be specified in the configuration file or can simply be commented out. 

Comments are marked with a hash symbol (`#`) at the beginning of the line. This is also useful to disable settings.

```ini
# This is a comment and is ignored
# setting=This is a setting that is also ignored
setting=This setting is used
```

## Data types used

Data types are specified for the settings in this configuration file. Unless otherwise specified, the following values are allowed:

| Type | Description |
| ---- | ----------- |
| Text | Any text can be specified here. |
| Boolean | Here the values 'true' or 'false' can be used to enable or disable a functionality. |
| Number | Any integer numbers can be specified here. Comma numbers are not allowed and are not used by any settings so far. If necessary, the setting specifies which range of values can be processed. |
| Time | This data type is actually intended for very large numbers and is used for time periods in this configuration file. The usage is described in more detail in the respective settings. |

## Basic information about Goobi Workflow

There is some basic information about the installed Goobi Workflow instance and about Goobi in general, specified in the configuration and partially displayed on the login page in the web browser.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `ApplicationTitle` | Text | `http://goobi.io` | The URL specified here leads to the general Goobi web page. There you can find more information about Goobi Workflow, the Goobi Viewer and Goobi-to-go. The documentation and the community section are also linked there. |
| `ApplicationHeaderTitle` | Text | `Goobi workflow` | The name of the software is entered here. It will be displayed on the Goobi Workflow login page. |
| `ApplicationHomepageMsg` | Text | | Here you can optionally specify the URL of an associated home page for the currently installed Goobi Workflow instance. |
| `ApplicationWebsiteMsg` | Text | | The URL of an associated website for the currently installed Goobi Workflow instance can optionally be specified here. |
| `developing` | Boolean | `false`| This switch indicates whether Goobi Workflow is in development mode. On production systems this value is always `false`. |

## Directories

Some directory paths can be set in the configuration file. Most of them are specified relative to the Goobi directory. The Goobi directory is usually located in `/opt/digiverso/goobi/`.

Some directories contain the text sequence `{processtitle}`. This is used in the respective directory names to insert the automatically generated title of a process. This ensures that the corresponding directories are created and used separately for each process.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `goobiFolder` | Text | `/opt/digiverso/goobi/` | This is the root directory of Goobi. It contains common directories such as `config/`, `plugins/`, `rulesets/` etc. |
| `dataFolder` | text | `metadata/` | All files of processes are stored in this directory. |
| `dir_Users` | Text | `users/` | This directory contains information about Goobi users. |
| `debugFolder` | Text | | This directory can be used to write an intermediate result to an XML file when importing Opac data. This is created in the directory specified here under the name `opacBeautifyAfter.xml`. |
| `folder_journal_internal` | Text | `internal` | Process log files are stored in this directory. **This value replaces the value `folder_processlog_internal` and is preferred if both values are used. |
| `folder_processlog_internal` | Text | `internal` | Process log files are stored in this directory. **This value is deprecated and was replaced with `folder_journal_internal`, but is still supported for compatibility reasons. |
| `doneDirectoryName` | Text | `finished/` | Files to be uploaded to other systems can be copied to this directory. The directory and all files in it will be deleted after the upload. |
| `useSwapping` | Boolean | `false` | This parameter specifies whether more space should be made available on external disks. |
| `swapPath` | Text | | The "swap" directory is used to have more space available on the current system. The directory is usually located on a network hard disk or an external disk that must be mounted in the operating system before use. To use swapping, `useSwapping=true` must be set. |
| `process.folder.images.master` | text | `{processtitle}_master` | This directory is used to store the original images for the respective process. |
| `process.folder.images.main` | Text | `{processtitle}_media` | In this directory additional data for the respective process will be stored. |
| `process.folder.images.source` | Text | `{processtitle}_source` | Additional resources for the respective process are stored in this directory. |
| `process.folder.images.fallback` | Text | | This directory contains files that are created during the processing of the process and are to be processed later. |
| `process.folder.images.[name]` | Text | | At this point any other `[name]` values can be used to provide further directories for different applications, for example also plugins. |
| `process.folder.ocr.txt` | Text | `{processtitle}_txt` | This directory is used to store `TXT` files for OCR processing. |
| `process.folder.ocr.pdf` | Text | `{processtitle}_pdf` | This directory contains `PDF` files for OCR processing. |
| `process.folder.ocr.xml` | Text | `{processtitle}_xml` | This directory contains `XML` files for OCR processing. |
| `process.folder.ocr.alto` | Text | `{processtitle}_alto` | This directory contains additional files for OCR processing. |
| `process.folder.import` | Text | `import` | Files for importing processes are stored in this directory. |
| `process.folder.export` | Text | `export` | Files for exporting processes are stored in this directory. |
| `createOrigFolderIfNotExists` | Boolean | `true` | This value can be set to `true` to automatically create the `master` directory for processes if it does not exist yet. |
| `createSourceFolder` | Boolean | `false` | This value can be set to `true` to create the directory named in `process.folder.images.source` if it does not exist yet. |

## General user settings

All custom user settings are stored by Goobi Workflow in the internally used database. The settings specified here are relevant for pages where no user is logged in (for example, the login page) and therefore the user-specific settings do not exist. Other settings in this category apply to all users and are not account-specific customizable.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `defaultLanguage` | Text | | This setting can be used to specify the default language of the Goobi Workflow user interface. This language will be used before a user is logged in and the language set for him/her will be loaded. The language abbreviations of the languages available on the Goobi Workflow instance can be used as language. By default these are `de`, `en`, `es`, `fr`, `it`, `iw`, `nl` and `pt`. |
| `anonymize` | Boolean | `false`| This switch can be set to `true` if the names of other users should be hidden in statistics and step and process details. |
| `enableGravatar` | Boolean | `true` | This switch can be used to specify whether profile pictures are used for users. Profile pictures are specified in the user accounts. If this setting is enabled and a user has no profile picture, the Goobi logo will be used by default. |

### Minimum password length

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `minimumPasswordLength` | Number | `8` | This value specifies the minimum password length for users. If a length less than 1 is specified, this value is replaced by 1. |

The password length is only checked when creating an account and when changing the own password. Existing passwords that are too short can still be used as long as this value is increased afterwards.

Administrators have the possibility to generate a new random password for users. These are always generated 10 characters longer than the minimum password length.

### Additional user permissions

Additional user permissions can be specified. For this purpose, a new entry with the 'userRight' property is made for each added permission. Thus, this value can occur multiple times and will be interpreted as a list by Goobi Workflow. 

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `userRight` | Text | | This setting can be used to add additional user permissions. |

This could look like this

```ini
userRight=Statistics_Latest
userRight=Statistics_Most_Relevant
userRight=Statistics_Users
```

**Note:** You should not enter user permissions whose name already exists in Goobi Workflow. This can lead to wrong behavior of some functions.

## Additional functionalities in the user interface

Goobi Workflow allows some optional functionalities for the user interface in the web browser. For this purpose there are the following switches that can be set to 'true' to enable functionalities:

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `ui_useIntrandaUI` | Boolean | `true` | This switch can be used to set whether the Intranda web interface is used as user interface. Nowadays this switch is always `true` |
| `renderAccessibilityCss` | Boolean | `false` | This switch sets whether an accessible design is loaded by default (for example on the login page). This is useful if some users depend on the accessible design and the user-specific accessible design is not yet loaded on the login page. |
| `showStatisticsOnStartPage` | Boolean | `true` | This switch can be set to show statistics on the start page (after login). |
| `TaskEnableFinalizeButton` | Boolean | `true` | This switch can be set if a user should have a button in the user interface to complete steps by himself. |
| `ui_showFolderLinkingInProcessList` | Boolean | `false` | This switch can be set to show extended download buttons for tasks in the task list. |
| `confirmLinking` | Boolean | `false` | This switch can be set to interpose a confirmation prompt before executing scripts. |
| `renderReimport` | Boolean | `false` | This switch can be set to display a button when downloading a process that allows to re-import the process. |

The following setting is used to filter the list of displayed sessions in the session overview. The setting itself can be used multiple times, each time specifying a client name (for example browser name) to be **filtered** from the session list.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `excludeMonitoringAgentName` | Text | | This setting specifies a name of a client which should **not** be displayed in the session list. |

For example, this looks like this if there are multiple names:

```ini
excludeMonitoringAgentName=Munin
excludeMonitoringAgentName=munin
excludeMonitoringAgentName=nagios-plugins
excludeMonitoringAgentName=monitoring-plugins
excludeMonitoringAgentName=ELB-HealthChecker/2.0
excludeMonitoringAgentName=python-requests
```

## Activate LDAP

The actual LDAP configuration is located in the database used by Goobi Workflow. In this database, there is a data record with numerous setting options for each LDAP group used. Whether LDAP is included can be controlled with the following parameter.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `ldap_use` | Boolean | `false` | This value indicates whether an LDAP service should be used. |

## Configure truststore

The truststore is used in Goobi Workflow to manage certificates and SSH keys. These can be used, for example, for authentication to the LDAP server or to other servers. To use the truststore, the following values must be configured.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `truststore` | Text | | This value specifies where the truststore is located. |
| `truststore_password` | Text | | This value specifies the password for authentication in the truststore. |

## OpenID Connect

Normally, user accounts are stored in the mariadb database managed by Goobi Workflow. Additionally there is the possibility to authenticate users with OpenID accounts.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `useOpenIdConnect` | Boolean | `false` | Setting this value to `true` will enable the ability to login with OpenID Connect in Goobi Workflow. |
| `OIDCAutoRedirect` | Boolean | `false` | If this value is set to `true`, the login page will be redirected directly to the login page of the OpenID provider. After successful login, this redirects directly back to Goobi Workflow. |
| `OIDCAuthEndpoint` | Text | | This specifies the API endpoint (URL or URI) used to authenticate the user. Specifying this value also configures the provider of the OpenID service. |
| `OIDCLogoutEndpoint` | Text | | Since a second API endpoint is used for logout, it must be explicitly specified here. This endpoint is also specified in the form of a URL or URI. |
| `OIDCIssuer` | Text | | The issue service of the OpenID provider is configured here.|
| `OIDCJWKSet` | Text | | The JWK service of the OpenID provider is configured here.|
| `OIDCClientID` | Text | | This specifies the client id that Goobi Workflow uses against the OpenID service. |
| `OIDCIdClaim` | Text | `email` | The value specified here can be set in the user database in the `ssoId` column to allow Goobi Workflow to use or ignore the OpenID service depending on the account. |
| `useOIDCSSOLogout` | Boolean | `false` | If this value is set to `true`, the user will be redirected to an intermediate page after successfully logging out. |

## Single Sign On (SSO)

SSO can be used to allow and configure authentication via HTTP headers. This allows or disallows staying logged in to a session in the browser using HTTP header fields.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `EnableHeaderLogin` | Boolean | `false` | Setting this value to `true` will enable SSO login in Goobi Workflow. |
| `SsoParameterType` | Text | `header` | This value determines where exactly the `SsoHeaderName` will be searched. If `header` is specified here, the value will be searched in the HTTP header errors. If `attribute` is specified here, the value will be searched in the URL parameters. |
| `SsoHeaderName` | Text| `Casauthn` | The text specified here will be requested as HTTP header field. The value sent in this field will be read and must match the SSO ID. |
| `showSSOLogoutPage` | Boolean | `false` | If this value is set to `true`, a corresponding intermediate page will be displayed after logout.|

## Set up external users

The following settings can be used to determine whether users with external accounts can be logged in to the system and, if so, how default values should be set that otherwise exist for normal accounts in the database.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `EnableExternalUserLogin` | Boolean | `false` | If this value is set to `true`, people with external accounts can log in to the system. |
| `ExternalUserDefaultInstitution` | Text | | Since external accounts are not assigned to any institution, an alternative institution name for all external accounts can be specified here. |
| `ExternalUserDefaultAuthentication` | Text | | Here you can specify an LDAP group to which users with external accounts should be assigned by default. |

## Database settings

In Goobi Workflow it is possible to search for specific terms in processes, tasks and other records. Since the search is handled by the SQL database used in the background, there are some settings available to adapt the search to the needs of each project.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `useFulltextSearch` | Boolean | `false` | If this switch is set to `true`, a full text search is performed that searches all database entries instead of a simple search using titles and a few metadata. |
| `FulltextSearchMode` | Text | `BOOLEAN MODE` | The search mode can be used to specify how to search the database. If `BOOLEAN MODE` is specified, regex-like expressions are used for searching. An alternative value is `NATURAL LANGUAGE MODE`. In this mode the search term (even with syntactically special characters) is searched directly in the text. |
| `DatabaseLeftTruncationCharacter` | Text | `%` | This character (or character string) is used as **prefix** in a database search query in connection with the SQL command `LIKE`. A `%` used as a prefix stands for any other text that can occur **before** the search term. |
| `DatabaseRightTruncationCharacter` | Text | `%` | This character (or character string) is used as **suffix** in a database search query in connection with the SQL command `LIKE`. A `%` used as suffix stands for any other text that can occur **after** the search term. |
| `SqlTasksIndexname` | Text | | An SQL index can be used for the search. The name of the index used is specified here. |

For the settings `DatabaseLeftTruncationCharacter` and `DatabaseRightTruncationCharacter`, `%` is specified in each case. This will cause the database search to be performed with SQL as follows (This example is for illustration purposes only and does not work this way in the actual database):

```sql
SELECT Title FROM Book WHERE Book.Title LIKE "%search term%";
```

This selects all records in which the search term occurs at any position. For example, if you omit the prefix `%` and search for `search term%`, you can search at the beginning of a record. This means, for example, that all books beginning with "The" can be searched for. If the prefix and suffix are omitted, only the search term is searched for and all records are selected that exactly match the search term.

To make database searches easier, aliases can be defined to group multiple properties together as one meta-property. For example, when searching for a person, it would be quite time-consuming to search for all authors, publishers, clerks, other persons, etc. For this reason, search terms can be listed and grouped under one name.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `index.***` | Text | | This value can be used to specify a comma-separated list of terms to be summarized under the term specified in `***`. The value can be used multiple times to make multiple summaries. |

For example, following aliases could be configured:

```ini
index.Person=Author, OtherPerson, Publisher, Editor
index.Institution=University, Museum, Archive
```

## Processes and process log

The following settings can be used to set the process log and some details for the editing of processes.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `ProcessCreationResetJournal` | Boolean | `false` | This value can be set to `true` to not copy the process log when duplicating a process. **This value replaces the value `ProcessCreationResetLog` and is preferred if both are used. |
| `ProcessCreationResetLog` | Boolean | `false` | This value can be set to `true` to not copy the process log when duplicating a process. **This value is deprecated and was replaced with `ProcessCreationResetJournal`, but is still supported for compatibility reasons. |
| `dir_allowWhiteSpaces` | Boolean | `false` | This value is set to `true` to allow spaces in file and directory names when creating or uploading files or directories. It is generally recommended to leave this setting at `false` because scripts in particular often cannot handle spaces in directory or file names and then the space is interpreted as a separator between two parameters. If `false` is set here, however, all spaces will be replaced internally by underscores to avoid the problem mentioned above. |
| `massImportAllowed` | Boolean | `false` | This value can be set to `true` to enable uploading of very large amounts of data. |
| `MassImportUniqueTitle` | Boolean | `true` | This value is set to `true` to allow only files with different names when uploading files. This simplifies later handling because then no name conflicts can occur. |
| `batchMaxSize` | Number | `100` | This value is used as limit for displaying batches and processes. |
| `ProcesslistShowEditionData` | Boolean | `false` | If this value is set to `true`, more information about process editing will be displayed in the process log. This includes information about the user who last worked on the process, when the process was last worked on, and which step was last worked on. |

### Configuration of jobs

For automatically executed background processes, it is possible to specify when they should be executed. The first three properties in the following list, marked with `daily`, are executed every day. The number of milliseconds specified is the time between 0:00 and the time the task is executed. This has the advantage that certain tasks can be executed at night, for example, when the load on the server is low.

The second advantage of this configuration is that the times of day can be set according to the difference between server time and the most used user time of day. This can happen when a server is located in another country (or uses UTC) and employees worldwide from different time zones work together on the server. 

If **-1** is specified, the corresponding job will be disabled.

The number of milliseconds can be calculated as follows:

* One second has 1000 milliseconds
* One minute has 60 seconds and thus 60 000 milliseconds
* One hour has 60 minutes and thus 3 600 000 milliseconds
* One day has 24 hours and thus 86 400 000 milliseconds.

So the given time should be between 0 and 86 400 000 to avoid errors. A few examples:

* For 0:00 o'clock 0 is indicated
* For 3:00 o'clock (3:00 AM) 3 * 3 600 000 = 10 800 000 is indicated
* For 18:30 (6:30 PM), 18 * 3 600 000 + 30 * 60 000 = 66 600 000 is given

For the setting 'goobiAuthorityServerUploadFrequencyInMinutes' a time in minutes is specified.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `dailyHistoryAnalyser` | Time | `-1` | This setting specifies when to backupt the processing of events from the last 24 hours. |
| `dailyDelayJob` | Time | `-1` | This setting determines when steps are executed for which a delay is enabled. |
| `dailyVocabJob` | Time | `-1` | This setting determines when the locally managed vocabulary is synchronized with other servers. |
| `goobiAuthorityServerUploadFrequencyInMinutes` | Time | `-1` | This value is used for requesting the authority server. Server requests are made in the background every n minutes, where n is the number of minutes specified here. For example, if 2 is specified, a request will be made every 2 minutes. |

### Downloadable information

In Goobi Workflow, **processes**, **templates**, **masterpieces** and **metadata** can not only be searched and displayed, but also exported to various file formats and downloaded. Some data from the database are already taken into account by default:

* `processes.Title` The title of a process
* `processes.processesID` The ID of a process
* `processes.creationdate` The creation date of a process
* `processes.sortHelperImages` The number of images in the process
* `processes.sortHelperMetadata` The number of metadata in the process
* `projects.title` The title of the project in which the process is located
* `log.lastError` The last detected error in the editing of this process

In addition, the `downloadAvailableColumn` setting can be used to include other properties in the exported files. For this purpose the mentioned setting can be used multiple times. All matching rows will be read in together by Goobi Workflow and processed as a coherent list.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `downloadAvailableColumn` | Text | | This specifies exactly one additional table column to be included in the export. |

In each line exactly one table column name from the Goobi database is specified. The following table columns are currently available (Goobi version 22.08):

* `prozesseeigenschaften.prozesseeigenschaftenID`
* `prozesseeigenschaften.Titel`
* `prozesseeigenschaften.WERT`
* `prozesseeigenschaften.IstObligatorisch`
* `prozesseeigenschaften.DatentypenID`
* `prozesseeigenschaften.Auswahl`
* `prozesseeigenschaften.prozesseID`
* `prozesseeigenschaften.creationDate`
* `prozesseeigenschaften.container`

* `vorlageneigenschaften.vorlageneigenschaftenID`
* `vorlageneigenschaften.Titel`
* `vorlageneigenschaften.WERT`
* `vorlageneigenschaften.IstObligatorisch`
* `vorlageneigenschaften.DatentypenID`
* `vorlageneigenschaften.Auswahl`
* `vorlageneigenschaften.vorlagenID`
* `vorlageneigenschaften.creationDate`
* `vorlageneigenschaften.container`

* `werkstueckeeigenschaften.werkstueckeeigenschaftenID`
* `werkstueckeeigenschaften.Titel`
* `werkstueckeeigenschaften.WERT`
* `werkstueckeeigenschaften.IstObligatorisch`
* `werkstueckeeigenschaften.DatentypenID`
* `werkstueckeeigenschaften.Auswahl`
* `werkstueckeeigenschaften.werkstueckeID`
* `werkstueckeeigenschaften.creationDate`
* `werkstueckeeigenschaften.container`

* `metadata.processid`
* `metadata.name`
* `metadata.value`
* `metadata.print`

It should be noted that only the column name is specified in the configuration. Otherwise the columns cannot be found, because the column names specified here are directly composed with the expected table names and searched. This has the side effect that by specifying for example 'Title' the title of processes, the title of templates and the title of masterpieces are taken into account.

For example, the following configuration can be made:

```ini
downloadAvailableColumn=Titel
downloadAvailableColumn=DatentypenID
downloadAvailableColumn=werkstueckeID
downloadAvailableColumn=name
downloadAvailableColumn=value
downloadAvailableColumn=print
```

This would result in the following additional table columns being used:

* `prozesseeigenschaften.Titel`
* `prozesseeigenschaften.DatentypenID`
* `vorlageneigenschaften.Titel`
* `vorlageneigenschaften.DatentypenID`
* `werkstueckeeigenschaften.Titel`
* `werkstueckeeigenschaften.DatentypenID`
* `metadata.name`
* `metadata.value`
* `metadata.print`

### Success and error messages for tasks

Manual tasks can be either completed successfully or set to error state by users in Goobi. In order to provide more information about the cause and resolution of errors, error and success messages can be pre-configured to be available later as a drop-down menu when completing (or canceling) tasks.

The following examples show how such messages can be used:

```ini
task.error.Missing\ pages=The following pages are missing: {}
task.error.Blurred\ images=The images {} are unsharp. Please create these again.
task.solution.Problem\ solved=The problem was solved. {}
task.solution.The\ original\ print\ is\ blurred=The original pages are printed blurry. It is not possible to create sharper images. {}
```

**Note:** Messages cannot be translated automatically and should be specified in a language that is understandable to as many users involved as possible. For international projects, English should be used.

Any number of messages can be specified. The respective drop-down menus are only available if at least one corresponding message is specified. All messages for error descriptions start with the prefix `task.error.`. All messages for problem fixes start with the prefix `task.solution.`.

After each prefix there is a short text which should be displayed as a dropdown item. Spaces must be escaped in it. After the equal sign follows a detailed description. This will be displayed later in the step details. At the placeholder `{}` the additionally specified remark (from the text field below the dropdown menu) will be inserted later.

## Scripts

Scripts can be configured to set up the file system. In a Goobi installation there are already suitable scripts included, but they are not set as default values here.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `script_createDirUserHome` | Text | | This script can be used to create and set up user directories. Example: `script_createDirUserHome.sh` |
| `script_createDirMeta` | Text | | This script can be used to create and set up the metadata directory. Example: `script_createDirMeta.sh` |
| `script_createSymLink` | Text | | This script can be used to create system links (to other directories or files). Example: `script_createSymLink.sh` |
| `script_deleteSymLink` | Text | | This script can be used to delete system links (to other directories or files). Example: `script_deleteSymLink.sh` | Text |

## Include S3 cloud

Amazon provides a cloud system where data objects can be stored in "buckets". This can be integrated by Goobi Workflow and used to exchange data with other servers.

To use S3, access data from the S3 service used is required. These must be specified in this configuration file.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `useS3` | Boolean | `false` | This value specifies whether an S3 store should be used. |
| `useCustomS3` | Boolean | `false` | This value specifies whether the `S3Endpoint`, `S3AccessKeyID` and `S3SecretAccessKey` settings specified in this configuration file should be used for selecting the S3 service and the necessary authentication. |
| `S3Endpoint` | Text | | This value specifies a domain name or IP address where the service can be reached. Usually a port number must be specified, for example: `http://123.123.123.123:9000` |
| `S3bucket` | Text | | This value specifies the name of the bucket used. |
| `S3AccessKeyID` | Text | | This value specifies the account ID that Goobi uses to access the service. |
| `S3SecretAccessKey` | Text | | This value specifies the access key or password that Goobi uses to identify itself for the account used. |
| `S3ConnectionRetry` | Number | `10` | This value specifies how many times to retry a failed interaction. |
| `S3ConnectionTimeout` | Number | `10000` | This value specifies how long to wait for a server response when connecting. The value is specified in milliseconds. |
| `S3SocketTimeout` | Number | `10000` | This value specifies how long to wait for a server response when interacting. The value is specified in milliseconds. |

## Proxy server settings

A Goobi server can use a proxy server for certain transactions with other servers or clients. By default, no proxy server is configured. To use a proxy server, you must first enable its use.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `http_proxyEnabled` | Boolean | `false` | This switch is set to `true` to enable the use of a proxy server. |
| `http_proxyUrl` | Text | | This value specifies the URL of the proxy server. |
| `http_proxyPort` | Number | `8080` | This value specifies the port number of the proxy server. |
| `http_proxyIgnoreHost` | Text | | Multiple IP addresses or URLs can be specified here to which Goobi connects without a proxy server. For this, this value may occur multiple times with one address each. |

The default values for `http_proxyIgnoreHost` are predefined as follows. The list can be extended as needed:

```ini
http_proxyIgnoreHost=localhost
http_proxyIgnoreHost=127.0.0.1
```

## Server and API settings

This category includes some settings that can be used to configure URLs and credentials to specific web services. Settings are also available to determine the behavior of the internal REST API. Especially for URLs, make sure to use the correct protocol (HTTP or HTTPS) and port number if the corresponding server or service uses one other than 80.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `useWebApi` | Boolean | `false` | This value can be set to `true` to enable Goobi Workflow's internal REST API. If it is disabled but still requested, a 404 Not Found Error will be returned with a corresponding error message. |
| `apiTokenSalt` | Text | | Here, an additional text can be specified that should be used as salt value for encrypting the authentication data for the REST API. |
| `jwtSecret` | Text | | The Goobi Workflow REST API uses a JSON Web Token (JWT) for authentication. This is specified here. To send an authenticated request to the REST API, the token must be specified in the request. |
| `goobiUrl` | Text | | The Goobi URL where the Goobi Workflow Server can be reached on the Internet can be specified here. This URL is only specified for internal purposes and can therefore also be set to `https://localhost:8080`. The protocol and port number should also be specified to avoid possible errors due to incorrect default values. |
| `pluginServerUrl` | Text | | The URL of the plugin server is specified here. The plugin server is also a REST API interface of the Goobi Workflow Server used to offer plugins for download. It is used by the integrated plugin management. |
| `ocrUrl` | Text | | This URL specifies an OCR service used by Goobi Workflow or OCR plugins to perform OCR analysis on a document.  |
| `goobiContentServerTimeOut` | Number | `60000` | This timeout (in milliseconds) specifies the time Goobi Workflow waits for a response from the content server. |
| `goobiAuthorityServerUrl` | Text | | This specifies the URL of the authority server used to manage vocabulary data. |
| `goobiAuthorityServerUser` | Text | | This specifies the user name used by Goobi Workflow to log in to the Authority server to retrieve vocabulary data. |
| `goobiAuthorityServerPassword` | Text | | This specifies the password used by Goobi Workflow to authenticate to the Authority server to retrieve vocabulary data. |
| `goobiAuthorityServerUploadFrequency` | Number | `0` | This specifies the frequency with which Goobi Workflow makes requests to the Authority server. |
| `geonames_account` | Text | | This value contains the authentication information that Goobi Workflow uses to authenticate itself to the Geonames web service for a query. |

## Configure message queues

Goobi Workflow uses multiple message queues to communicate with other processes on the same server (localhost) or other servers. ActiveMQ is always used for production use. For development purposes, SQS can be used in some cases. Since the entire constellation and configuration of the message queues is somewhat confusing, all configuration possibilities are documented here for the sake of completeness, even if individual constellations are not used on production systems. In each case, it is indicated which configurations are relevant for a production system.

### Message queues used

* Goobi Workflow uses one or more **slow** queues to transmit normal process communication notifications.
* There is a **fast** queue for transmitting particularly small or time-critical information.
* An **internal DLQ** (Dead Letter Queue) is used to catch undeliverable notifications on the same server.
* An **external DLQ** is used to catch undeliverable notifications between multiple servers.
* There is a separate queue for **commands** that can be sent either on the same server or between different servers. These can be executable scripts, for example.

### Simple Queue Service (SQS)

In principle, all queues can be operated with ActiveMQ. The **external DLQ** and the queue for **commands** have the special feature that they can work either with ActiveMQ or with SQS (Simple Queue Service). As long as ActiveMQ is used for these queues, it is possible to switch between a localhost service and an external service. The localhost service is set with default parameters and does not need to be configured further. If an external service is to be used or other individual configurations are to be made, this is configured in the file `goobi_activemq.xml`. The SQS service, on the other hand, is always located on the same server (localhost) and does not need to be configured. 

### Configuration

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `MessageBrokerStart` | Boolean | `false` | This value is set to `true` to enable the use of message queues in Goobi Workflow. |
| `ActiveMQConfig` | Text | goobiFolder + `config/goobi_activemq.xml` | A configuration file for ActiveMQ can be specified here. In this file also the URL and the port for the communication with other servers are configured. If this property is set and thus the default value is overwritten, an absolute path must be specified. |
| `MessageBrokerServer` | text | `localhost` | This setting is used by Spring Framework and specifies the URL (or `localhost`) of the ActiveMQ service. |
| `MessageBrokerPort` | Number | `61616` | This setting is used by Spring Framework and specifies the port of the ActiveMQ service. |
| `MessageBrokerUsername` | Text | | This is the account name that Goobi Workflow uses to register with ActiveMQ. |
| `MessageBrokerPassword` | Text | | This is the password Goobi Workflow uses to authenticate itself with ActiveMQ. |
| `MessageBrokerNumberOfParallelMessages` | Number | `1` | Here you can specify the number of slow message queues. With a higher value more data transmissions can be executed in parallel. A speed advantage arises especially with large amounts of data, if the used server has many processor cores and these are released by the operating system for Goobi or ActiveMQ. |
| `allowExternalQueue` | Boolean | `false` | If this setting is set to `true`, Goobi Workflow will also use a DLQ for communication with other servers, i.e. a queue for notifications that could not be sent without errors. |
| `externalQueueType` | Text | `activeMQ` | This value can be set to `activeMQ` or `SQS` to switch the queue service for the command queue and the external DLQ. **In production systems this is always `activeMQ`.**|
| `useLocalSQS` | Boolean | `false` | If the queue service is set to `SQS`, this parameter can be set to `true` to use the default connection used by Goobi Workflow via `http://localhost:9324`. Otherwise, a default configuration used by SQS will be used. **This setting is not used on production systems**.

Additionally the names of the respective queues can be configured. This is normally not required and is documented here for completeness.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `GOOBI_INTERNAL_FAST_QUEUE` | Text | `goobi_fast` | This is the queue for fast information exchange of small information units. |
| `GOOBI_INTERNAL_SLOW_QUEUE` | Text | `goobi_slow` | This is the queue (or several) for exchanging larger data packets. |
| `GOOBI_EXTERNAL_JOB_QUEUE` | Text | `goobi_external` | This is the queue for external communication with other servers. |
| `GOOBI_EXTERNAL_JOB_DLQ` | Text | `goobi_external.DLQ` | This is the queue for non-deliverable information generated by communication with other processes on other servers. |
| `GOOBI_EXTERNAL_COMMAND_QUEUE` | Text | `goobi_command` | This is the queue to send commands between servers. |
| `GOOBI_INTERNAL_DLQ` | Text | `ActiveMQ.DLQ` | This is the queue for non-deliverable information that is generated when communicating with other processes on the same server. |

## Metadata editor

The metadata editor has many setting options that can be sorted both technically and thematically. As a compromise, and because there is no "one" correct sorting, all settings are sorted by categories, such as "User Interface", "Export", etc. For OCR settings, for example, this means that showing/not showing the OCR button is configured in the "User Interface" section, while technical details about OCR are described in the "Export" section.

### General settings

In the General Settings you can find settings concerning the editor itself and default values for new documents.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `MetsEditorEnableDefaultInitialization` | Boolean | `true` | This value can be set to `true` to make default configurations in the document structure when loading a document in the metadata editor. |
| `MetsEditorEnableImageAssignment` | Boolean | `true` | This value can be set to `true` to enable automatic assignment of image files to a document structure. |
| `MetsEditorDefaultPagination` | Text | `uncounted` | This setting can be used to specify the default pagination system. Valid values are `arabic` (0, 1, 2, ..., 7, 8, 9), `roman` (I, V, X, L, C, D, M) and `uncounted` (no page numbers).  |
| `MetsEditorLockingTime` | Time | `180000` | This value specifies how long a document edited in the metadata editor is reserved for a user and locked for other users. The reservation is set to prevent multiple users from editing a document at the same time and overwriting changes made by other users unnoticed. The reservation is removed as soon as the user saves the document and leaves the metadata editor or the lock time has expired. The lock time is specified in milliseconds, the default value is half an hour and is calculated for example with `Lock time = 30 minutes * 60 seconds * 1000 milliseconds = 180000 milliseconds`. |
| `MetsEditorUseExternalOCR` | Boolean | `false` | This value can be set to `true` to use an external OCR service. This is configured with the `ocrUrl=address` setting. If the use of the external OCR service is disabled, the OCR equivalent text contents will be loaded directly from resource files. |
| `numberOfMetaBackups` | Number | `0` | This value specifies the number of backups of the `meta.xml` file and the `meta_anchor.xml` file. **Note:** If 0 is entered here, no backups will be stored. |

### User interface

The "User Interface" category documents settings that can be used to configure the display of content or the display/non-display of buttons.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `showOcrButton` | Boolean | `false` | This value can be set to `true` to display a button in the metadata editor for running the OCR analyze on the currently selected structure element. |
| `MetsEditorDisplayFileManipulation` | Boolean | `false` | This value can be set to `true` to display unsaved modified documents in the metadata editor. |
| `MetsEditorShowArchivedFolder` | Boolean | `false` | This value can be set to `true` to show archived image files. |
| `MetsEditorShowMetadataPopup` | Boolean | `true` | This value can be set to `true` to show a button that can be used to display additional metadata for a document in a popup. |
| `MetsEditorMaxTitleLength` | Number | `0` | This value specifies the maximum number of characters to be displayed in names of document structure elements. If a name is longer than the value specified here, only the first characters are displayed according to the maximum length. This value can be set to `0` to disable the maximum length. |

### Image files and thumbnails

This category documents settings for image files, thumbnails, the display of images, and the tiling of images in the user interface.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `ShowImageComments` | Boolean | `false` | This value can be set to `true` to show image comments for individual pages of documents. |
| `MetsEditorNumberOfImagesPerPage` | Number | `96` | This value specifies how many thumbnails are displayed on a page in the metadata editor by default. |
| `MetsEditorUseImageTiles` | Boolean | `true` | This value can be set to `true` to load image files on the user interface tile by tile. This allows a smoother display of the images. |
| `ImageSorting` | Text | `number` | This value specifies the criterion by which image file names are sorted. With the value `number` file names are sorted numerically (for example 1, 10, 30, 100, 200, 1000). With the value `alphanumeric` file names are sorted lexicographically (for example 1, 10, 100, 1000, 200, 30). |
| `ImagePrefix` | text | `\\d{8}` | This value can contain a regular expression (regex) and specifies which string image file names must start with to be accepted as valid files. The default prefix specifies that a file name must start with 8 digits (e.g. YYYYMMDD). |
| `UserForImageReading` | Text | `root` | Image files can be downloaded in read-only mode. These then do not belong to the user, but to another virtual user who provides the image files with read-only privileges. The username of this virtual user is configured with this value. Usually `root` is used. |
| `UseImageThumbnails` | Boolean | `true` | This value can be set to `true` to display thumbnails of document pages. |
| `MetsEditorThumbnailsize` | Number | `200` | This value specifies the size in pixels at which thumbnails are displayed in the metadata editor. |
| `MaxParallelThumbnailRequests` | Number | `100` | This value can be set to limit the number of thumbnails loaded simultaneously. This option is especially useful on weaker servers. |
| `MetsEditorMaxImageSize` | Number | `15000` | This value specifies the maximum image size in pixels that an image may have in order to be displayed in the metadata editor. |

The maximum size of image files (in bytes) is defined with two independently configurable values. With the value `MaxImageFileSize` a number is specified, such as `1`, `5` or `10`. With the additional value `MaxImageFileSizeUnit` the unit of measurement is specified. These in combination give the maximum number of bytes an image file may not exceed. **Important:** Only integer numbers can be used.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `MaxImageFileSize` | Number | `4000` | This value specifies the factor for the maximum image size in bytes. |
| `MaxImageFileSizeUnit` | Text | `MB` | This value specifies the unit of measurement by which the factor is multiplied to obtain the total image size in bytes. |

Since there are many misunderstood units of measurement, the following table lists all accepted values and their internally used numeric values.

| Unit | Factor | Description |
| ---- | ------ | ----------- |
| `B` | `1` | Byte |
| `K` or `KB` | `1000` | Kilobyte |
| `KI` or `KIB` | `1024` | Kibibyte |
| `M` or `MB` | `1000*1000` | Megabyte |
| `MI` or `MIB` | `1024*1024` | Mebibyte |
| `G` or `GB` | `1000*1000*1000` | Gigabyte |
| `GI` or `GIB` | `1024*1024*1024` | Gibibyte |
| `T` or `TB` | `1000*1000*1000*1000` | Terabyte |
| `TI` or `TIB` | `1024*1024*1024*1024` | Tebibyte |

This can be used, for example, to make the following settings:

```ini
# 20 Megabyte -> 20 * 1000 * 1000 = 20 000 000 Byte
MaxImageFileSize=20
MaxImageFileSizeUnit=MB
```

or

```ini
# 1 Gibibyte -> 1 * 1024 * 1024 * 1024 = 1 073 741 824 Byte
MaxImageFileSize=1
MaxImageFileSizeUnit=GIB
```

The following values can be used to configure information about supported image and tile sizes for JSON API requests. The following API request can be used to retrieve this information about images from operations:

```ini
/process/image/{process}/{folder}/{filename}/info.json
```

Thereby all values can be used multiple times and return multiple values in the API request.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `MetsEditorImageSize` | Text | | This value can be used to specify multiple sizes (in pixels) for common images. |
| `MetsEditorImageTileSize` | Text | | This value can be used to specify multiple sizes (in pixels) for tiles. |
| `MetsEditorImageTileScale` | Text | | This value can be used to specify multiple scaling sizes for tiles. |

For example, a configuration could look like this:

```ini
MetsEditorImageSize=4096

MetsEditorImageTileSize=64
MetsEditorImageTileSize=128
MetsEditorImageTileSize=256

MetsEditorImageTileScale=1
MetsEditorImageTileScale=32
```

When completing steps, various internal data checks are performed. Among other things, the number of existing and processed image files is checked. The `historyImageSuffix` value can be used to specify one or more file types that will be considered for this count.

This setting is used for file extensions and can also contain general texts with which a file name should end, but no regular expressions are interpreted.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `historyImageSuffix` | Text | `.tif` | This value can be used to specify one or more file types. |

For example, if all `*.tif`, `*.jpg` and `*.jpeg` files are to be considered, the following list could be used:

```ini
historyImageSuffix=.tif
historyImageSuffix=.jpg
historyImageSuffix=.jpeg
```

### Validation

This category contains settings for validating operations, image files and metadata.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `useMetadatavalidation` | Boolean | `true` | This value can be set to `true` to validate the metadata of the current document when saving and exiting the metadata editor. |
| `MetsEditorValidateImages` | Boolean | `true` | This value can be set to `true` to display a validate button in the metadata editor to allow user-initiated validation. |
| `validateProcessTitleRegex` | Text | `[\\w-]*` | This value specifies a regular expression (regex) to be used to check the validity of process titles. |
| `ProcessTitleGenerationRegex` | Text | `[\\W]` | This value specifies a regular expression (regex) to be used to remove invalid special characters from process titles. |

### Export

This category describes settings that affect the export of operations to downloadable files or files that can be cached on the server.

| Property | Type | Default value | Description |
| -------- | ---- | ------------- | ----------- |
| `ExportExiftoolPath` | Text | `/usr/bin/exiftool` | This specifies the file path and program name of the program used for extracting additional metadata (EXIF data) from image files. |
| `useOrigFolder` | Boolean | `true` | This value can be set to `true` to get image files directly from the master folder when importing. |
| `exportWithoutTimeLimit` | Boolean | `true` | This value can be set to `true` if export processes should not be subject to a time limit. |
| `ExportValidateImages` | Boolean | `true` | This value can be set to `true` to validate image files during export. |
| `ExportMetadataForProject` | Text | | Here, the name of the metadata field is specified where the name of the project should be exported to. |
| `ExportMetadataForInstitution` | Text | | Here, the name of the metadata field is specified where the name of the institution should be exported to. |
| `ExportMetadataForDfgViewerUrl` | Text | | Here, the name of the metadata field is specified where the URL of the DFG viewer should be exported to. |
| `ExportFilesFromOptionalMetsFileGroups` | Boolean | `false` | This value can be set to `true` to consider optional file groups when exporting. |
| `ExportInTemporaryFile` | Boolean | `false` | This value can be set to `true` to store exports in temporary files. |
| `ExportCreateUUID` | Boolean | `true` | This value can be set to `true` to set the UUID (universally unique identifier) of files when exporting. |
| `ExportCreateTechnicalMetadata` | Boolean | `false` | This value can be set to `true` to include additional technical metadata related to the document structure when exporting. |
| `automaticExportWithImages` | Boolean | `true` | This value can be set to `true` to include image files in automatic export processes. |
| `automaticExportWithOcr` | Boolean | `true` | This value can be set to `true` to perform OCR analysis during automatic export processes. |
| `pdfAsDownload` | Boolean | `true` | This value can be set to `true` to make exported PDF documents available for download. If this value is set to `false` exported PDF documents will be stored in the user folder of the corresponding user on the server. |