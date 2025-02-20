# goobi_config.properties

In der Konfigurationsdatei `goobi_config.properties` werden einige grundlegende Einstellungen für Goobi Workflow eingestellt. Die Datei befindet sich üblicherweise an folgendem Speicherpfad:

```bash
/opt/digiverso/goobi/config/goobi_config.properties
```

Beispielhaft sieht diese Konfigurationsdatei wie folgt aus:

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

## Allgemeines

Diese Konfigurationsdatei wird schon seit sehr langer Zeit in Goobi Workflow verwendet und beinhaltet daher teilweise veraltete Einstellungen, die heutzutage nur noch aus Kompatibilitätsgründen unterstützt werden. Diese sind gesondert gekennzeichnet und beschreiben gegebenenfalls eine Alternative, wie diese Einstellungen zu ersetzen sind.

Da die Einstellungen über einen langen Zeitraum ergänzt wurden und immer noch werden, haben sich immer wieder andere Namenskonventionen in den Variablennamen bewährt. Daher muss insbesondere auf den richtigen Gebrauch von Groß- und Kleinschreibung sowie Unterstrichen und Punkten in den Variablennamen geachtet werden.

Diese Konfigurationsdatei beinhaltet Einstellungen zu vielen unterschiedlichen Themen. Teilweise lässt es sich nicht vermeiden, dass bestimmte Einstellungen zu mehreren Themen passen und je nach Anwendungszweck auch in verschiedenen Kategorien stehen können. Sollten bestimmte Einstellungen nicht an der erwarteten Stelle wiederzufinden sein, wird empfohlen, mit der Suchfunktion des Browsers (üblicherweise Strg+F) die Seite zu durchsuchen.

Viele Einstellungen haben Standardwerte, die so gewählt sind, dass sie für die meisten Anwender sinnvoll sind. Daher müssen nicht alle Einstellungen in der Konfigurationsdatei angegeben werden oder können einfach auskommentiert werden. 

Kommentare werden mit einem Raute-Symbol (`#`) am Zeilenanfang markiert. Dies ist auch nützlich, um Einstellungen zu deaktivieren.

```ini
# Dies ist ein Kommentar und wird ignoriert
# setting=Dies ist eine Einstellung, die auch ignoriert wird
setting=Diese Einstellung wird verwendet
```

## Verwendete Datentypen

Für die Einstellungen in dieser Konfigurationsdatei sind Datentypen angegeben. Sofern es nicht anders angegeben ist, sind folgende Werte zulässig:

| Typ | Beschreibung |
| --- | -------------- |
| Text | Hier können beliebige Texte angegeben werden. |
| Boolean | Hier können die Werte `true` oder `false` verwendet werden, um eine Funktionalität ein- oder auszuschalten. |
| Number | Hier können beliebige Ganzzahlen angegeben werden. Kommazahlen sind nicht erlaubt und werden auch bisher von keinen Einstellungen verwendet. Sofern erforderlich, wird bei der jeweiligen Einstellung angegeben, welcher Wertebereich verarbeitet werden kann. |
| Time | Dieser Datentyp ist eigentlich für sehr große Zahlen bestimmt und wird in dieser Konfigurationsdatei für Zeiträume verwendet. Der Gebrauch ist in den betreffenden Einstellungen genauer beschrieben. |

## Basisinformationen über Goobi Workflow

Es gibt einige grundlegende Informationen über die installierte Goobi Workflow-Instanz und über Goobi allgemein, die in der Konfiguration angegeben und teilweise auf der Login-Seite im Webbrowser angezeigt werden.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `ApplicationTitle` | Text | `http://goobi.io` | Die hier angegebene URL führt zur allgemeinen Webseite von Goobi. Dort befinden sich mehr Informationen über Goobi Workflow, den Goobi Viewer und Goobi-to-go. Außerdem sind dort die Dokumentation und der Community-Bereich verlinkt. |
| `ApplicationHeaderTitle` | Text | `Goobi workflow` | Hier wird der Name der Software eingetragen. Dieser wird auf der Login-Seite von Goobi Workflow angezeigt. |
| `ApplicationHomepageMsg` | Text | | Hier kann optional die URL einer zugehörigen Homepage für die aktuell installierte Goobi Workflow Instanz angegeben werden. |
| `ApplicationWebsiteMsg` | Text | | Hier kann optional die URL einer zugehörigen Webseite für die aktuell installierte Goobi Workflow Instanz angegeben werden. |
| `developing` | Boolean | `false`| Dieser Schalter gibt an, ob sich Goobi Workflow im Entwicklungsmodus befindet. Auf Produktivsystemen ist dieser Wert immer `false`. |

## Verzeichnisse

Es können einige Verzeichnispfade in der Konfigurationsdatei gesetzt werden. Die meisten davon werden relativ zum Goobi-Verzeichnis angegeben. Das Goobi-Verzeichnis befindet sich üblicherweise in `/opt/digiverso/goobi/`.

Einige Verzeichnisse beinhalten die Textsequenz `{processtitle}`. Diese wird in den jeweiligen Verzeichnisnamen verwendet, um den automatisch generierten Titel eines Vorgangs einzusetzen. Damit wird erreicht, dass die entsprechenden Verzeichnisse für jeden Vorgang separat angelegt und verwendet werden.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `goobiFolder` | Text | `/opt/digiverso/goobi/` | Dies ist das Hauptverzeichnis von Goobi. Darin befinden sich übliche Verzeichnisse, wie zum Beispiel `config/`, `plugins/`, `rulesets/` usw. |
| `dataFolder` | Text | `metadata/` | In diesem Verzeichnis werden alle Dateien von Vorgängen gespeichert. |
| `dir_Users` | Text | `users/` | Dieses Verzeichnis beinhaltet Informationen über Goobi-Nutzer. |
| `debugFolder` | Text | | Dieses Verzeichnis kann verwendet werden, um beim Import von Opac-Daten ein Zwischenergebnis in eine XML-Datei zu schreiben. Diese wird in dem hier angegebenen Verzeichnis unter dem Namen `opacBeautifyAfter.xml` angelegt. |
| `folder_journal_internal` | Text | `intern` | In diesem Verzeichnis werden Vorgangslog-Dateien gespeichert. **Dieser Wert ersetzt den Wert `folder_processlog_internal` und wird bevorzugt, wenn beide verwendet werden. |
| `folder_processlog_internal` | Text | `intern` | In diesem Verzeichnis werden Vorgangslog-Dateien gespeichert. **Dieser Wert ist veraltet und wurde durch `folder_journal_internal` ersetzt, wird aber noch aus Kompatibilitätsgründen unterstützt. |
| `doneDirectoryName` | Text | `fertig/` | In dieses Verzeichnis können Dateien kopiert werden, die auf andere Systeme hochgeladen werden sollen. Das Verzeichnis und alle darin befindlichen Dateien werden nach dem Upload gelöscht. |
| `useSwapping` | Boolean | `false` | Mit diesem Parameter wird angegeben, ob mehr Speicherplatz auf externen Datenträgern zur Verfügung gestellt werden soll. |
| `swapPath` | Text | | Das "swap"-Verzeichnis wird verwendet, um mehr Speicherplatz auf dem aktuellen System zur Verfügung zu haben. Das Verzeichnis befindet sich üblicherweise auf einer Netzwerkfestplatte oder einem externen Datenträger, der vor Gebrauch im Betriebssystem eingebunden ("gemountet") werden muss. Um das Swapping zu benutzen, muss `useSwapping=true` gesetzt werden. |
| `process.folder.images.master` | Text | `{processtitle}_master` | In diesem Verzeichnis werden die Originalbilder für den jeweiligen Vorgang gespeichert. |
| `process.folder.images.main` | Text | `{processtitle}_media` | In diesem Verzeichnis werden weitere Daten zu dem jeweiligen Vorgang gespeichert. |
| `process.folder.images.source` | Text | `{processtitle}_source` | In diesem Verzeichnis werden weitere Ressourcen für den jeweiligen Vorgang gespeichert. |
| `process.folder.images.fallback` | Text | | Dieses Verzeichnis beinhaltet Dateien, die bei der Abarbeitung des Vorgangs entstehen und später weiterverarbeitet werden sollen. |
| `process.folder.images.[name]` | Text | | An dieser Stelle können weitere beliebige `[name]`-Werte verwendet werden, um weitere Verzeichnisse für verschiedene Anwendungen, zum Beispiel auch Plugins, zur Verfügung zu stellen. |
| `process.folder.ocr.txt` | Text | `{processtitle}_txt` | In diesem Verzeichnis werden `TXT`-Dateien für eine OCR-Bearbeitung abgelegt. |
| `process.folder.ocr.pdf` | Text | `{processtitle}_pdf` | In diesem Verzeichnis werden `PDF`-Dateien für eine OCR-Bearbeitung abgelegt. |
| `process.folder.ocr.xml` | Text | `{processtitle}_xml` | In diesem Verzeichnis werden `XML`-Dateien für eine OCR-Bearbeitung abgelegt. |
| `process.folder.ocr.alto` | Text | `{processtitle}_alto` | In diesem Verzeichnis werden weitere Dateien für eine OCR-Bearbeitung abgelegt. |
| `process.folder.import` | Text | `import` | In diesem Verzeichnis werden Dateien zum Import von Vorgängen gespeichert. |
| `process.folder.export` | Text | `export` | In diesem Verzeichnis werden Dateien zum Export von Vorgängen gespeichert. |
| `createOrigFolderIfNotExists` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um das `master`-Verzeichnis für Vorgänge automatisch anzulegen, wenn es noch nicht existiert. |
| `createSourceFolder` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um das in `process.folder.images.source` genannte Verzeichnis zu erstellen, wenn es noch nicht existiert. |

## Allgemeine Nutzer-Einstellungen

Alle benutzerdefinierten Nutzereinstellungen speichert Goobi Workflow in der intern verwendeten Datenbank. Die hier angegebenen Einstellungen sind für Seiten relevant, auf denen kein Nutzer angemeldet ist (zum Beispiel die Login-Seite) und daher die nutzerspezifischen Einstellungen nicht existieren. Andere Einstellungen in dieser Kategorie gelten für alle Nutzer und sind nicht accountspezifisch anpassbar.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `defaultLanguage` | Text | | Mit dieser Einstellung kann die Standardsprache von der Goobi Workflow Benutzeroberfläche angegeben werden. Diese Sprache wird verwendet, bevor ein Benutzer angemeldet ist und die für ihn eingestellte Sprache geladen wird. Als Sprache können die Sprachkürzel der auf der Goobi Workflow Instanz zur Verfügung stehenden Sprachen verwendet werden. Standardmäßig sind das `de`, `en`, `es`, `fr`, `it`, `iw`, `nl` und `pt`. |
| `anonymize` | Boolean | `false`| Dieser Schalter kann auf `true` gesetzt werden, wenn in Statistiken und Schritt- und Vorgangs-Details die Namen anderer Benutzer ausgeblendet werden sollen. |
| `enableGravatar` | Boolean | `true` | Mit diesem Schalter kann angegeben werden, ob für Benutzer Profilbilder verwendet werden. Profilbilder werden in den Nutzeraccounts spezifiziert. Ist diese Einstellung aktiviert und hat ein Nutzer kein Profilbild, so wird standardmäßig das Goobi-Logo verwendet. |

### Minimale Passwort-Länge

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `minimumPasswordLength` | Number | `8` | Dieser Wert gibt die minimale Passwortlänge für Benutzer an. Wird eine Länge angegeben, der kleiner als 1 ist, so wird dieser Wert durch 1 ersetzt. |

Die Passwort-Länge wird nur beim Anlegen eines Accounts und beim Ändern des eigenen Passwortes geprüft. Bestehende und zu kurze Passwörter können weiter genutzt werden, sofern dieser Wert im Nachhinein erhöht wird.

Für Administratoren besteht die Möglichkeit, ein neues zufälliges Passwort für Nutzer zu generieren. Diese werden immer 10 Zeichen länger generiert, als es die minimale Passwort-Länge vorgibt.

### Weitere Benutzerberechtigungen

Es können weitere Benutzerberechtigungen angegeben werden. Dazu wird für jede hinzugefügte Berechtigung ein neuer Eintrag mit der Eigenschaft `userRight` vorgenommen. Somit kann dieser Wert mehrfach vorkommen und wird von Goobi Workflow als Liste interpretiert. 

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `userRight` | Text | | Mit dieser Einstellung können weitere Benutzerberechtigungen hinzugefügt werden. |

Das kann zum Beispiel so aussehen:

```ini
userRight=Statistics_Latest
userRight=Statistics_Most_Relevant
userRight=Statistics_Users
```

**Hinweis:** Es sollten keine Benutzerberechtigungen eingetragen werden, deren Bezeichnung bereits in Goobi Workflow existieren. Dies kann zu falschem Verhalten von einigen Funktionen führen.

## Zusätzliche Funktionen in der Benutzeroberfläche

Goobi Workflow lässt einige optionale Funktionalitäten für die Benutzeroberfläche im Webbrowser zu. Dafür gibt es folgende Schalter, die auf `true` gesetzt werden können, um Funktionalitäten zu aktivieren:

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `ui_useIntrandaUI` | Boolean | `true` | Mit diesem Schalter kann eingestellt werden, ob die Intranda Weboberfläche als Benutzeroberfläche verwendet wird. Dieser Schalter ist heutzutage immer `true` |
| `renderAccessibilityCss` | Boolean | `false` | Mit diesem Schalter wird eingestellt, ob standardmäßig (zum Beispiel auf der Login-Seite) ein barrierefreies Design geladen wird. Dies ist hilfreich, wenn einige Anwender auf das barrierefreie Design angewiesen sind und auf der Login-Seite noch nicht das nutzerspezifisch eingestellte barrierefreie Design geladen wird. |
| `showStatisticsOnStartPage` | Boolean | `true` | Dieser Schalter kann gesetzt werden, um Statistiken auf der Startseite (nach dem Login) anzuzeigen. |
| `TaskEnableFinalizeButton` | Boolean | `true` | Dieser Schalter kann gesetzt werden, wenn ein Benutzer in der Benutzeroberfläche einen Button haben soll, um selbstständig Schritte abzuschließen. |
| `ui_showFolderLinkingInProcessList` | Boolean | `false` | Dieser Schalter kann gesetzt werden, um erweiterte Download-Buttons für Vorgänge in der Vorgänge-Liste anzuzeigen. |
| `confirmLinking` | Boolean | `false` | Dieser Schalter kann gesetzt werden, um vor dem Ausführen von Scripts eine Sicherheitsabfrage zwischenzuschalten. |
| `renderReimport` | Boolean | `false` | Dieser Schalter kann gesetzt werden, um beim Herunterladen eines Vorgangs einen Button anzuzeigen, der das Wieder-Importieren des Vorgangs ermöglicht. |

Die folgende Einstellung wird verwendet, um die Liste der angezeigten Sessions in der Session-Übersicht zu filtern. Die Einstellung selbst kann mehrfach verwendet werden, wobei jedes Mal ein Client-Name (zum Beispiel Browser-Name) angegeben wird, der aus der Session-Liste **herausgefiltert** werden soll.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `excludeMonitoringAgentName` | Text | | Mit dieser Einstellung wird ein Name eines Clients angegeben, der **nicht** in der Session-Liste angezeigt werden soll. |

Das sieht bei mehreren Namen zum Beispiel so aus:

```ini
excludeMonitoringAgentName=Munin
excludeMonitoringAgentName=munin
excludeMonitoringAgentName=nagios-plugins
excludeMonitoringAgentName=monitoring-plugins
excludeMonitoringAgentName=ELB-HealthChecker/2.0
excludeMonitoringAgentName=python-requests
```

## LDAP aktivieren

Die eigentliche LDAP-Konfiguration befindet sich in der von Goobi Workflow verwendeten Datenbank. In dieser gibt es für jede verwendete LDAP-Gruppe einen Datensatz mit zahlreichen Einstellungsmöglichkeiten. Ob LDAP eingebunden wird, ist mit folgendem Parameter steuerbar.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `ldap_use` | Boolean | `false` | Dieser Wert gibt an, ob ein LDAP-Service verwendet werden soll. |

## Truststore konfigurieren

Der Truststore wird in Goobi Workflow verwendet, um Zertifikate und SSH-Schlüssel zu verwalten. Diese können zum Beispiel für die Authentifikation am LDAP-Server oder an anderen Servern verwendet werden. Um den Truststore verwenden zu können, ist die Konfiguration folgender Werte erforderlich.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `truststore` | Text |  | Dieser Wert gibt an, wo sich der Truststore befindet. |
| `truststore_password` | Text |  | Dieser Wert gibt das Passwort für die Authentifizierung im Truststore an. |

## OpenID Connect

Normalerweise werden Benutzeraccounts in der von Goobi Workflow verwalteten mariadb-Datenbank gespeichert. Zusätzlich gibt es die Möglichkeit, Benutzer mit OpenID-Accounts zu authentifizieren.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `useOpenIdConnect` | Boolean | `false` | Wird dieser Wert auf `true` gesetzt, so wird die Möglichkeit des Logins mit OpenID Connect in Goobi Workflow freigeschaltet. |
| `OIDCAutoRedirect` | Boolean | `false` | Wird dieser Wert auf `true` gesetzt, so wird beim Aufrufen der Login-Seite direkt zur Login-Seite des OpenID Anbieters weitergeleitet. Nach erfolgreichem Login leitet dieser direkt zurück zu Goobi Workflow. |
| `OIDCAuthEndpoint` | Text | | Hier wird der API-Endpoint (URL oder URI) angegeben, mit der die Authentifizierung des Nutzers vorgenommen wird. Mit Angabe dieses Wertes wird zugleich der Anbieter des OpenID-Services konfiguriert. |
| `OIDCLogoutEndpoint` | Text | | Da für das Abmelden ein zweiter API-Endpoint verwendet wird, muss dieser hier explizit angegeben werden. Auch dieser Endpoint wird in Form einer URL oder URI angegeben. |
| `OIDCIssuer` | Text | | Hier wird der Issue-Service des OpenID-Anbieters konfiguriert.|
| `OIDCJWKSet` | Text | | Hier wird der JWK-Service des OpenID-Anbieters konfiguriert.|
| `OIDCClientID` | Text | | Hier wird die Client id angegeben, die Goobi Workflow gegenüber dem OpenID Service nutzt. |
| `OIDCIdClaim` | Text | `email` | Der hier angegebene Wert kann in der Datenbank für Benutzer in der Spalte `ssoId` gesetzt werden, damit Goobi Workflow accountabhängig den OpenID Service nutzen oder ignorieren kann. |
| `useOIDCSSOLogout` | Boolean | `false` | Wird dieser Wert auf `true` gesetzt, so wird der Nutzer nach erfolgreichem Abmelden auf eine Zwischenseite weitergeleitet. |

## Single Sign On (SSO)

Mit SSO kann eine Authentifizierung über HTTP-Header zugelassen und konfiguriert werden. Diese erlaubt oder verbietet es, mittels HTTP-Header-Feldern bei einer Sitzung im Browser angemeldet zu bleiben.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `EnableHeaderLogin` | Boolean | `false` | Wird dieser Wert auf `true` gesetzt, so wird der SSO-Login in Goobi Workflow freigeschaltet. |
| `SsoParameterType` | Text | `header` | Dieser Wert bestimmt, wo genau der `SsoHeaderName` gesucht wird. Wird hier `header` angegeben, so wird der Wert in den HTTP-Header-Fehldern gesucht. Wird hier `attribute` angegeben, so wird der Wert in den URL-Parametern gesucht. |
| `SsoHeaderName` | Text| `Casauthn` | Der hier angegebene Text wird als HTTP-Headerfeld abgefragt. Der in diesem Feld mitgeschickte Wert wird ausgelesen und muss der SSO-ID entsprechen. |
| `showSSOLogoutPage` | Boolean | `false` | Wird dieser Wert auf `true` gesetzt, so wird nach dem Abmelden eine entsprechende Zwischenseite angezeigt.|

## Externe Benutzer einrichten

Mit den folgenden Einstellungen kann bestimmt werden, ob Benutzer mit externen Accounts am System angemeldet werden können und wie gegebenenfalls Standardwerte gesetzt werden sollen, die sonst für normale Accounts in der Datenbank existieren.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `EnableExternalUserLogin` | Boolean | `false` | Wird dieser Wert auf `true` gesetzt, so können sich Personen mit externen Accounts am System anmelden. |
| `ExternalUserDefaultInstitution` | Text | | Da externe Accounts keiner Institution zugeordnet sind, kann hier eine alternative Institutionsbezeichnung für alle externen Accounts angegeben werden. |
| `ExternalUserDefaultAuthentication` | Text | | Hier kann eine LDAP-Gruppe angegeben werden, der Nutzer mit externen Accounts standardmäßig zugeordnet werden sollen. |

## Datenbank-Einstellungen

In Goobi Workflow kann in Vorgängen, Aufgaben und anderen Datensätzen nach bestimmten Begriffen gesucht werden. Da die Suche von der im Hintergrund verwendeten SQL-Datenbank übernommen wird, stehen einige Einstellungen zur Verfügung, um die Suche an den Bedarf der jeweiligen Projekte anzupassen.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `useFulltextSearch` | Boolean | `false` | Wird dieser Schalter auf `true` gesetzt, so wird statt einer einfachen Suche über Titel und wenige Metadaten eine Volltextsuche durchgeführt, die alle Datenbankeinträge durchsucht. |
| `FulltextSearchMode` | Text | `BOOLEAN MODE` | Mit dem Suchmodus kann angegeben werden, wie in der Datenbank gesucht wird. Wird `BOOLEAN MODE` angegeben, so wird mit regex-ähnlichen Ausdrücken gesucht. Ein alternativer Wert ist `NATURAL LANGUAGE MODE`. In diesem Modus wird der Suchbegriff (auch mit syntaktisch besonderen Zeichen) direkt im Text gesucht. |
| `DatabaseLeftTruncationCharacter` | Text | `%` | Dieses Zeichen (bzw. Zeichenfolge) wird als **Präfix** bei einer Datenbank-Suchanfrage im Zusammenhang mit dem SQL-Befehl `LIKE` verwendet. Dabei steht ein als Präfix verwendetes `%` für einen beliebigen anderen Text, der **vor** dem Suchbegriff vorkommen kann. |
| `DatabaseRightTruncationCharacter` | Text | `%` | Dieses Zeichen (bzw. Zeichenfolge) wird als **Suffix** bei einer Datenbank-Suchanfrage im Zusammenhang mit dem SQL-Befehl `LIKE` verwendet. Dabei steht ein als Suffix verwendetes `%` für einen beliebigen anderen Text, der **nach** dem Suchbegriff vorkommen kann. |
| `SqlTasksIndexname` | Text | | Für das Suchen kann ein SQL-Index verwendet werden. Der Name des verwendeten Index wird an dieser Stelle angegeben. |

Bei den Einstellungen `DatabaseLeftTruncationCharacter` und `DatabaseRightTruncationCharacter` wird jeweils `%` angegeben. Das führt dazu, dass die Suche in der Datenbank mit SQL wie folgt ausgeführt wird (Dieses Beispiel dient lediglich der Veranschaulichung und funktioniert nicht so in der eigentlichen Datenbank):

```sql
SELECT Title FROM Book WHERE Book.Title LIKE "%suchbegriff%";
```

Es werden damit also alle Datensätze ausgewählt, in denen der Suchbegriff an beliebiger Stelle vorkommt. Wird zum Beispiel der Präfix `%` weggelassen und nach `suchbegriff%` gesucht, so kann am Anfang eines Datensatzes gesucht werden. Damit kann zum Beispiel nach allen Büchern gesucht werden, die mit "The" anfangen. Werden Präfix und Suffix weggelassen, so wird nur noch nach dem Suchbegriff gesucht und es werden alle Datensätze ausgewählt, die exakt dem Suchbegriff entsprechen.

Um Datenbanksuchen einfacher zu machen, können Aliasse definiert werden, mit denen mehrere Eigenschaften als eine Metaeigenschaft zusammengefasst werden. Wenn man zum Beispiel nach einer Person sucht, wäre es recht aufwändig, nach allen Autoren, Veröffentlichern, Sachbearbeitern, anderen Personen usw. zu suchen. Aus diesem Grund können Suchbegriffe aufgelistet und unter einem Namen zusammengefasst werden.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `index.***` | Text | | Mit diesem Wert kann eine kommagetrennte Liste von Begriffen angegeben werden, die unter dem in `***` genannten Begriff zusammengefasst werden sollen. Der Wert kann mehrfach verwendet werden, um mehrere Zusammenfassungen vorzunehmen. |

Zum Beispiel könnten folgende Aliasse konfiguriert werden:

```ini
index.Person=Author, OtherPerson, Publisher, Editor
index.Institution=University, Museum, Archive
```

## Vorgänge und Vorgangslog

Mit den folgenden Einstellungen können das Vorgangs-Log und einige Details zur Bearbeitung von Vorgängen eingestellt werden.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `ProcessCreationResetJournal` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um beim Duplizieren eines Vorgangs das Vorgangslog nicht mitzukopieren. **Dieser Wert ersetzt den Wert `ProcessCreationResetLog` und wird bevorzugt, falls beide vewendet werden. |
| `ProcessCreationResetLog` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um beim Duplizieren eines Vorgangs das Vorgangslog nicht mitzukopieren. **Dieser Wert ist veraltet und wurde durch `ProcessCreationResetJournal` ersetzt, wird aber aus Kompatibilitätsgründen noch unterstützt. |
| `dir_allowWhiteSpaces` | Boolean | `false` | Dieser Wert wird auf `true` gesetzt, um beim Anlegen oder Hochladen von Dateien oder Ordnern Leerzeichen in Datei- und Ordnernamen zuzulassen. Es wird im allgemeinen empfohlen, diese Einstellung bei `false` zu belassen, da insbesondere Scripts oft nicht mit Leerzeichen in Ordner- oder Dateinamen umgehen können und dann das Leerzeichen als Trennzeichen zwischen zwei Parametern interpretiert wird. Wird hier hingegen `false` eingestellt, so werden intern alle Leerzeichen durch Unterstriche ersetzt, um das genannte Problem zu vermeiden. |
| `massImportAllowed` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um das Hochladen von sehr großen Datenmengen freizuschalten. |
| `MassImportUniqueTitle` | Boolean | `true` | Dieser Wert wird auf `true` gesetzt, um beim Hochladen von Dateien nur Dateien mit unterschiedlichen Namen zu erlauben. Das vereinfacht die spätere Handhabung, da dann keine Namenskonflikte mehr auftreten können. |
| `batchMaxSize` | Number | `100` | Dieser Wert wird als Limit für die Anzeige von Batches und Vorgängen verwendet. |
| `ProcesslistShowEditionData` | Boolean | `false` | Wird dieser Wert auf `true` gesetzt, so werden mehr Informationen zur Bearbeitung von Vorgängen in der Vorgangsübersicht angezeigt. Dies beinhaltet Informationen über den Nutzer, der zuletzt an dem Vorgang gearbeit hat, wann zuletzt am Vorgang gearbeitet wurde und welcher Schritt zuletzt bearbeitet wurde. |

### Konfiguration von Jobs

Für automatisch ausgeführte Hintergrundprozesse kann angegeben werden, wann diese ausgeführt werden sollen. Die ersten drei Eigenschaften in der folgenden Liste, gekennzeichnet mit `daily`, werden jeden Tag ausgeführt. Die angegebene Zahl an Millisekunden ist die Zeit zwischen 0:00 Uhr und dem Zeitpunkt der Ausführung der Aufgabe. Das hat den Vorteil, dass bestimmte Aufgaben zum Beispiel nachts ausgeführt werden können, wenn die Auslastung des Servers gering ist.

Der zweite Vorteil dieser Konfiguration ist, dass die Tageszeiten entsprechend der Differenz zwischen Serverzeit und der meistbenutzten Nutzer-Tageszeit eingestellt werden können. Das kann vorkommen, wenn ein Server in einem anderen Land steht (oder UTC benutzt) und Mitarbeiter weltweit aus verschiedenen Zeitzonen zusammen auf dem Server arbeiten. 

Wird **-1** angegeben, so wird der entsprechende Job deaktiviert.

Die Anzahl der Millisekunden kann wie folgt berechnet werden:

* Eine Sekunde hat 1000 Millisekunden
* Eine Minute hat 60 Sekunden und damit 60 000 Millisekunden
* Eine Stunde hat 60 Minuten und damit 3 600 000 Millisekunden
* Ein Tag hat 24 Stunden und damit 86 400 000 Millisekunden

Der angegebene Zeitpunkt sollte also zwischen 0 und 86 400 000 liegen, um Fehler zu vermeiden. Ein paar Beispiele:

* Für 0:00 Uhr wird 0 angegeben
* Für 3:00 Uhr (3:00 AM) wird 3 * 3 600 000 = 10 800 000 angegeben
* Für 18:30 Uhr (6:30 PM) wird 18 * 3 600 000 + 30 * 60 000 = 66 600 000 angegeben

Für die Einstellung `goobiAuthorityServerUploadFrequencyInMinutes` wird eine Zeit in Minuten angegeben.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `dailyHistoryAnalyser` | Time | `-1` | Mit dieser Einstellung wird festgelegt, wann die Bearbeitung von Vorgängen der letzten 24 Stunden gebackupt werden soll. |
| `dailyDelayJob` | Time | `-1` | Mit dieser Einstellung wird festgelegt, wann Schritte ausgeführt werden, für die ein Delay (Zeitverzögerung) eingeschaltet ist. |
| `dailyVocabJob` | Time | `-1` | Mit dieser Einstellung wird festgelegt, wann das lokal verwaltete Vokabular mit anderen Servern synchronisiert wird. |
| `goobiAuthorityServerUploadFrequencyInMinutes` | Time | `-1` | Dieser Wert wird für das Anfragen des Authority-Servers verwendet. Es werden im Hintergrund alle n Minuten Serveranfragen gestellt, wobei n die hier angegebene Minutenzahl ist. Wird zum Beispiel 2 angegeben, so wird alle 2 Minuten eine Anfrage gestellt. |

### Herunterladbare Informationen

In Goobi Workflow können **Vorgänge**, **Vorlagen**, **Werkstücke** und **Metadaten** nicht nur gesucht und angezeigt, sondern auch in verschiedene Dateiformate exportiert und heruntergeladen werden. Dabei werden einige Daten aus der Datenbank standardmäßig bereits berücksichtigt:

* `prozesse.Titel` Der Titel eines Vorgangs
* `prozesse.ProzesseID` Die ID eines Vorgangs
* `prozesse.erstellungsdatum` Das Erstellungsdatum eines Vorgangs
* `prozesse.sortHelperImages` Die Anzahl an Bildern im Vorgang
* `prozesse.sortHelperMetadata` Die Anzahl an Metadaten im Vorgang
* `projekte.Titel` Der Titel des Projektes, in dem sich der Vorgang befindet
* `log.lastError` Der zuletzt erkannte Fehler in der Bearbeitung dieses Vorgangs

Zusätzlich können mit der Einstellung `downloadAvailableColumn` weitere Eigenschaften in den exportierten Dateien berücksichtigt werden. Dafür kann die genannte Einstellung mehrfach verwendet werden. Alle passenden Zeilen werden von Goobi Workflow zusammen eingelesen und als zusammenhängende Liste weiterverarbeitet.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `downloadAvailableColumn` | Text | | Hier wird genau eine weitere Tabellenspalte angegeben, die beim Export berücksichtigt werden soll. |

In jeder Zeile wird genau ein Tabellen-Spaltenname aus der Goobi-Datenbank angegeben. Zur Verfügung stehen aktuell (Goobi Version 22.08) folgende Tabellenspalten:

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

Zu beachten ist, dass nur der Spaltenname in der Konfiguration angegeben wird. Andernfalls können die Spalten nicht gefunden werden, da die hier angegebenen Spaltennamen direkt mit den erwarteten Tabellennamen zusammengesetzt und gesucht werden. Das hat den Seiteneffekt, dass durch die Angabe von zum Beispiel `Titel` der Titel von Vorgängen, der Titel von Vorlagen und der Titel von Werkstücken berücksichtigt werden.

Es kann zum Beispiel folgende Konfiguration vorgenommen werden:

```ini
downloadAvailableColumn=Titel
downloadAvailableColumn=DatentypenID
downloadAvailableColumn=werkstueckeID
downloadAvailableColumn=name
downloadAvailableColumn=value
downloadAvailableColumn=print
```

Dies würde dazu führen, dass zusätzlich folgende Tabellenspalten verwendet werden:

* `prozesseeigenschaften.Titel`
* `prozesseeigenschaften.DatentypenID`
* `vorlageneigenschaften.Titel`
* `vorlageneigenschaften.DatentypenID`
* `werkstueckeeigenschaften.Titel`
* `werkstueckeeigenschaften.DatentypenID`
* `metadata.name`
* `metadata.value`
* `metadata.print`

### Erfolgs- und Fehlermeldungen für Aufgaben

Manuelle Aufgaben können von Benutzern in Goobi entweder erfolgreich abgeschlossen oder in den Fehlerzustand versetzt werden. Um mehr Informationen über die Ursache und die Behebung von Fehlern zur Verfügung zu stellen, können Fehler- und Erfolgsmeldungen vorkonfiguriert werden, die später beim Abschließen (oder Abbrechen) von Aufgaben als Dropdown-Menü zur Verfügung stehen sollen.

Folgende Beispiele zeigen, wie solche Meldungen verwendet werden können:

```ini
task.error.Missing\ pages=The following pages are missing: {}
task.error.Blurred\ images=The images {} are unsharp. Please create these again.
task.solution.Problem\ solved=The problem was solved. {}
task.solution.The\ original\ print\ is\ blurred=The original pages are printed blurry. It is not possible to create sharper images. {}
```

**Hinweis:** Die Meldungen können nicht automatisch übersetzt werden und sollten in einer Sprache angegeben werden, die für möglichst alle beteiligten Nutzer verständlich ist. Bei internationalen Projekten sollte Englisch verwendet werden.

Es können beliebig viele Meldungen angegeben werden. Die jeweiligen Dropdown-Menüs stehen nur zur Verfügung, wenn mindestens eine entsprechende Meldung angegeben ist. Alle Meldungen für Fehlerbeschreibungen beginnen mit dem Präfix `task.error.`. Alle Meldungen für Problembehebungen beginnen mit dem Präfix `task.solution.`.

Nach dem jeweiligen Präfix kommt ein kurzer Text, der als Dropdown-Item angezeigt werden soll. Leerzeichen müssen darin escaped werden. Nach dem Gleichheitszeichen folgt eine ausführliche Beschreibung. Diese wird später in den Schritt-Details angezeigt. An dem Platzhalter `{}` wird später die zusätzlich angegebene Bemerkung (aus dem Textfeld unterhalb des Dropdown-Menüs) eingesetzt.

## Scripts

Es können Scripts zum Einrichten des Dateisystems konfiguriert werden. In einer Goobi Installation sind bereits passende Scripts enthalten, diese sind hier allerdings nicht als Standardwerte gesetzt.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `script_createDirUserHome` | Text | | Mit diesem Script können Benutzerverzeichnisse erstellt und eingerichtet werden. Beispiel: `script_createDirUserHome.sh` |
| `script_createDirMeta` | Text | | Mit diesem Script kann das Metadatenverzeichnis erstellt und eingerichtet werden. Beispiel: `script_createDirMeta.sh` |
| `script_createSymLink` | Text | | Mit diesem Script können System-Links (zu anderen Verzeichnissen oder Dateien) erstellt werden. Beispiel: `script_createSymLink.sh` |
| `script_deleteSymLink` | Text | | Mit diesem Script können System-Links (zu anderen Verzeichnissen oder Dateien) gelöscht werden. Beispiel: `script_deleteSymLink.sh` |

## S3 Cloud einbinden

Amazon stellt ein Cloud-System zur Verfügung, in dem Datenobjekte in "Buckets" gespeichert werden können. Dieses kann von Goobi Workflow eingebunden und zum Austausch von Daten mit anderen Servern verwendet werden.

Für die Nutzung von S3 sind Zugangsdaten vom verwendeten S3-Service erforderlich. Diese müssen in dieser Konfigurationsdatei angegeben werden.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `useS3` | Boolean | `false` | Dieser Wert gibt an, ob ein S3-Speicher verwendet werden soll. |
| `useCustomS3` | Boolean | `false` | Dieser Wert gibt an, ob die in dieser Konfigurationsdatei angegebenen Einstellungen `S3Endpoint`, `S3AccessKeyID` und `S3SecretAccessKey` für die Auswahl des S3 Services und die notwendige Authentifizierung verwendet werden sollen. |
| `S3Endpoint` | Text | | Dieser Wert gibt beinhaltet einen Domainnamen oder eine IP Adresse, unter der der Service erreichbar ist. Üblicherweise muss eine Portnummer angegeben werden, zum Beispiel: `http://123.123.123.123:9000` |
| `S3bucket` | Text | | Dieser Wert gibt den Namen des verwendeten Buckets an. |
| `S3AccessKeyID` | Text | | Dieser Wert gibt die Account-ID an, mit der Goobi auf den Service zugreift. |
| `S3SecretAccessKey` | Text | | Dieser Wert gibt den Zugangsschlüssel bzw. Passwort an, mit dem sich Goobi für den verwendeten Account identifiziert. |
| `S3ConnectionRetry` | Number | `10` | Dieser Wert gibt an, wie oft versucht werden soll, eine fehlgeschlagene Interaktion erneut zu versuchen. |
| `S3ConnectionTimeout` | Number | `10000` | Dieser Wert gibt an, wie lange beim Verbinden auf eine Serverantwort gewartet werden soll. Der Wert wird in Millisekunden angegeben. |
| `S3SocketTimeout` | Number | `10000` | Dieser Wert gibt an, wie lange bei Interaktionen auf eine Serverantwort gewartet werden soll. Der Wert wird in Millisekunden angegeben. |

## Proxy-Server-Einstellungen

Ein Goobi Server kann für bestimmte Transaktionen mit anderen Servern oder Clients einen Proxy-Server verwenden. Standardmäßig ist kein Proxy-Server konfiguriert. Um einen Proxy-Server verwenden zu können, muss zunächst die Verwendung aktiviert werden.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `http_proxyEnabled` | Boolean | `false` | Dieser Schalter wird auf `true` gesetzt, um die Verwendung eines Proxy-Servers zu aktivieren. |
| `http_proxyUrl` | Text | | Dieser Wert gibt die URL des Proxy-Servers an. |
| `http_proxyPort` | Number | `8080` | Dieser Wert gibt die Portnummer des Proxy-Servers an. |
| `http_proxyIgnoreHost` | Text | `localhost`, `127.0.0.1` | Es können mehrere IP-Adressen oder URLs angegeben werden, zu denen Goobi eine Verbindung ohne Proxy-Server aufbaut. Dafür kann dieser Wert mehrfach verwendet werden, wobei jeweils eine Adresse angegeben wird. |

Die Standardwerte für `http_proxyIgnoreHost` sind wie folgt vordefiniert. Die Liste kann je Bedarf ergänzt werden.

```ini
http_proxyIgnoreHost=localhost
http_proxyIgnoreHost=127.0.0.1
```

## Server- und API-Einstellungen

Diese Kategorie umfasst einige Einstellungen, mit denen URLs und Zugangsdaten zu bestimmten Webservices konfiguriert werden können. Außerdem sind Einstellungen verfügbar, mit denen das Verhalten der internen REST-API bestimmt werden kann. Insbesondere bei URL-Angaben ist auf das richtige Protokoll (HTTP oder HTTPS) und auf die Port-Nummer zu achten, sofern der entsprechende Server bzw. Service eine andere als 80 verwendet.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `useWebApi` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um die interne REST-API von Goobi Workflow freizuschalten. Ist sie ausgeschaltet und wird trotzdem angefragt, so wird ein 404 Not Found Error mit einer entsprechenden Fehlermeldung zurückgegeben. |
| `apiTokenSalt` | Text | | Hier kann ein zusätzlicher Text angegeben werden, der als Salt-Wert für die Verschlüsselung der Authentifizierungsdaten für die REST-API verwendet werden soll. |
| `jwtSecret` | Text | | Die REST-API von Goobi Workflow verwendet zur Authentifizierung ein JSON Web Token (JWT). Dieses wird hier spezifiziert. Um eine authentifizierte Anfrage an die REST-API zu schicken, muss das Token in der Anfrage angegeben werden. |
| `goobiUrl` | Text | | Hier kann die Goobi URL angegeben werden, unter der der Goobi Workflow Server im Internet erreichbar ist. Diese URL wird nur für interne Zwecke angegeben und kann daher auch auf `https://localhost:8080` gesetzt werden. Das Protokoll und die Portnummer sollten mit angegeben werden, um eventuelle Fehler durch falsche Standardwerte zu vermeiden. |
| `pluginServerUrl` | Text | | Hier wird die URL des Plugin-Servers angegeben. Der Plugin-Server ist ebenfalls eine REST-API-Schnittstelle des Goobi Workflow Servers, die dafür verwendet wird, Plugins zum Download anzubieten. Sie wird von der integrierten Plugin-Verwaltung verwendet. |
| `ocrUrl` | Text | | Diese URL gibt einen OCR-Service an, der von Goobi Workflow bzw. OCR-Plugins verwendet wird, um die OCR-Analyse auf einem Dokument auszuführen.  |
| `goobiContentServerTimeOut` | Number | `60000` | Dieses Timeout (in Millisekunden) gibt die Zeit an, die Goobi Workflow auf eine Antwort vom Content-Server wartet. |
| `goobiAuthorityServerUrl` | Text | | Hier wird die URL des Authority-Servers angegeben, der für die Verwaltung von Vokabular-Daten verwendet wird. |
| `goobiAuthorityServerUser` | Text | | Hier wird der verwendete Nutzer-Name angegeben, den Goobi Workflow für die Anmeldung am Authority-Server verwendet, um Vokabular-Daten abzufragen. |
| `goobiAuthorityServerPassword` | Text | | Hier wird das verwendete Passwort angegeben, das Goobi Workflow für die Authentifizierung am Authority-Server verwendet, um Vokabular-Daten abzufragen. |
| `goobiAuthorityServerUploadFrequency` | Number | `0` | Hier wird die Häufigkeit angegeben, mit der Goobi Workflow Anfragen an den Authority-Server stellt. |
| `geonames_account` | Text | | Dieser Wert beinhaltet die Authentifizierungsinformationen, die Goobi Workflow verwendet, um sich für eine Suchanfrage beim Geonames-Webservice zu authentifizieren. |

## Message Queues konfigurieren

Goobi Workflow verwendet mehrere Message Queues, um mit anderen Prozessen auf dem selben Server (localhost) oder anderen Servern zu kommunizieren. Dabei wird im Produktiveinsatz immer ActiveMQ verwendet. Zu Entwicklungszwecken kann teilweise SQS verwendet werden. Da die gesamte Konstellation und Konfiguration der Message Queues etwas unübersichtlich ist, sind hier der Vollständigkeit halber alle Konfigurationsmöglichkeiten dokumentiert, auch wenn einzelne Konstellationen nicht auf Produktivsystemen zum Einsatz kommen. Es ist jeweils angegeben, welche Konfigurationen für ein Produktivsystem relevant sind.

### Verwendete Message Queues

* Goobi Workflow verwendet eine oder mehrere **langsame** Queues zur Übertragung von normalen Benachrichtigungen im Bereich der Prozesskommunikation.
* Es gibt eine **schnelle** Queue zum Übertragen von besonders kleinen bzw. zeitlich kritischen Informationen.
* Eine **interne DLQ** (Dead Letter Queue) wird verwendet, um nicht zustellbare Benachrichtigungen auf dem selben Server aufzufangen.
* Eine **externe DLQ** wird verwendet, um nicht zustellbare Benachrichtigungen zwischen mehreren Servern aufzufangen.
* Es gibt eine eigene Queue für **Befehle**, die entweder auf dem selben Server oder zwischen verschiedenen Servern verschickt werden können. Das können zum Beispiel ausführbare Scripts sein.

### Simple Queue Service (SQS)

Grundsäzlich können alle Queues mit ActiveMQ betrieben werden. Die **externe DLQ** und die Queue für **Befehle** haben die Besonderheit, dass sie entweder mit ActiveMQ oder mit SQS (Simple Queue Service) funktionieren können. Solange für diese Queues ActiveMQ verwendet wird, kann zwischen einem localhost-Service und einem externen Service umgeschaltet werden. Der localhost-Service ist mit Standardparametern belegt und muss nicht weiter konfiguriert werden. Soll ein externer Service verwendet werden oder andere individuelle Konfigurationen vorgenommen werden, so wird dies in der Datei `goobi_activemq.xml` konfiguriert. Der SQS-Service hingegen befindet sich immer auf dem selben Server (localhost) und muss nicht konfiguriert werden. 

### Konfiguration

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `MessageBrokerStart` | Boolean | `false` | Dieser Wert wird auf `true` gesetzt, um den Gebrauch von Message Queues in Goobi Workflow zu aktivieren. |
| `ActiveMQConfig` | Text | goobiFolder + `config/goobi_activemq.xml` | Hier kann eine Konfigurationsdatei für ActiveMQ angegeben werden. In dieser werden auch die URL und der Port für die Kommunikation mit anderen Servern konfiguriert. Wird diese Eigenschaft gesetzt und damit der Standardwert überschrieben, so ist ein absoluter Pfad anzugeben. |
| `MessageBrokerServer` | Text | `localhost` | Diese Einstellung wird vom Spring Framework verwendet und gibt die URL (oder `localhost`) des ActiveMQ Services an. |
| `MessageBrokerPort` | Number | `61616` | Diese Einstellung wird vom Spring Framework verwendet und gibt den Port des ActiveMQ Services an. |
| `MessageBrokerUsername` | Text | | Dies ist der Accountname, mit dem sich Goobi Workflow bei ActiveMQ registriert. |
| `MessageBrokerPassword` | Text | | Dies ist das Passwort, mit dem sich Goobi Workflow bei ActiveMQ authentifiziert. |
| `MessageBrokerNumberOfParallelMessages` | Number | `1` | Hier kann die Anzahl an langsamen Message Queues angegeben werden. Mit einem höheren Wert können mehr Datenübertragungen parallel ausgeführt werden. Ein Geschwindigkeitsvorteil entsteht gerade bei großen Datenmengen dann, wenn der verwendete Server viele Prozessorkerne hat und diese vom Betriebssystem für Goobi bzw. ActiveMQ freigegeben sind. |
| `allowExternalQueue` | Boolean | `false` | Wird diese Einstellung auf `true` gesetzt, so verwendet Goobi Workflow auch für die Kommunikation mit anderen Servern eine DLQ, also eine Warteschlange für Benachrichtigungen, die nicht fehlerfrei verschickt werden konnten. |
| `externalQueueType` | Text | `activeMQ` | Dieser Wert kann auf `activeMQ` oder `SQS` gesetzt werden, um den Queue-Service für die Befehls-Queue und die externe DLQ umzuschalten. **In Produktivsystemen ist dies immer `activeMQ`. |
| `useLocalSQS` | Boolean | `false` | Ist der Queue-Service auf `SQS` eingestellt, so kann dieser Parameter auf `true` gesetzt werden, um die von Goobi Workflow verwendeten Standard-Verbindung über `http://localhost:9324` zu verwenden. Anderfalls wird eine von SQS verwendete Standardkonfiguration verwendet. **Diese Einstellung wird nicht auf Produktivsystemen verwendet. |

Es können zusätzlich die Namen der jeweiligen Queues konfiguriert werden. Dies ist normalerweise nicht erforderlich und ist hier der Vollständigkeit halber dokumentiert.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `GOOBI_INTERNAL_FAST_QUEUE` | Text | `goobi_fast` | Dies ist die Warteschlange für schnellen Informationsaustausch von kleinen Informationseinheiten. |
| `GOOBI_INTERNAL_SLOW_QUEUE` | Text | `goobi_slow` | Dies ist die Warteschlange (bzw. mehrere) für dem Austausch von größeren Datenpaketen. |
| `GOOBI_EXTERNAL_JOB_QUEUE` | Text | `goobi_external` | Dies ist die Warteschlange für externe Kommunikation mit anderen Servern. |
| `GOOBI_EXTERNAL_JOB_DLQ` | Text | `goobi_external.DLQ` | Dies ist die Warteschlange für nicht-zustellbare Informationen, die bei der Kommunikation mit anderen Prozessen auf anderen Servern anfallen. |
| `GOOBI_EXTERNAL_COMMAND_QUEUE` | Text | `goobi_command` | Dies ist die Warteschlange, mit der Befehle zwischen Servern verschickt werden können. |
| `GOOBI_INTERNAL_DLQ` | Text | `ActiveMQ.DLQ` | Dies ist die Warteschlange für nicht-zustellbare Informationen, die bei der Kommunikation mit anderen Prozessen auf dem selben Server anfallen. |

## Metadateneditor

Der Metadateneditor hat viele Einstellungsmöglichkeiten, die sich sowohl technisch, als auch thematisch sortieren lassen können. Als Kompromiss, und weil es nicht "die" richtige Sortierung gibt, sind alle Einstellungen nach Kategorien, wie zum Beispiel "Benutzeroberfläche", "Export", usw. sortiert. Für OCR-Einstellungen heißt das zum Beispiel, dass das Anzeigen/Nicht Anzeigen des OCR-Buttons im Bereich "Benutzeroberfläche" konfiguriert wird, während technische Details zum OCR im Bereich "Export" beschrieben sind.

### Allgemeine Einstellungen

In den Allgemeinen Einstellungen sind Einstellungen zu finden, die den Editor selbst und Standardwerte für neue Dokumente betreffen.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `MetsEditorEnableDefaultInitialization` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um beim Laden eines Dokuments im Metadateneditor Standardkonfigurationen in der Dokumentstruktur vorzunehmen. |
| `MetsEditorEnableImageAssignment` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um eine automatische Zuordnung von Bilddateien zu einer Dokumentstruktur zu aktivieren. |
| `MetsEditorDefaultPagination` | Text | `uncounted` | Mit dieser Einstellung kann das Standard-Zahlensystem für die Seitenzählung angegeben werden. Gültige Werte sind `arabic` (0, 1, 2, ..., 7, 8, 9), `roman` (I, V, X, L, C, D, M) und `uncounted` (keine Seitenzahlen).  |
| `MetsEditorLockingTime` | Time | `180000` | Dieser Wert gibt an, wie lange ein im Metadateneditor bearbeitetes Dokument für einen Nutzer reserviert und für andere Nutzer gesperrt ist. Die Reservierung wird gesetzt, damit nicht mehrere Nutzer gleichzeitig ein Dokument bearbeiten und Änderungen anderer Nutzer unbemerkt überschrieben werden. Die Reservierung wird aufgehoben, sobald der Benutzer das Dokument speichert und den Metadateneditor verlässt oder die Sperrzeit abgelaufen ist. Die Sperrzeit wird in Millisekunden angegeben, der Standardwert beträgt eine halbe Stunde und errechnet sich beispielsweise mit `Sperrzeit = 30 Minuten * 60 Sekunden * 1000 Millisekunden = 180000 Millisekunden`. |
| `MetsEditorUseExternalOCR` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um einen externen OCR-Service zu verwenden. Dieser wird mit der Einstellung `ocrUrl=address` konfiguriert. Ist die Nutzung des externen OCR-Service deaktiviert, so werden die OCR-äquivalenten Textinhalte direkt aus Ressourcen-Dateien geladen. |
| `numberOfMetaBackups` | Number | `0` | Mit diesem Wert wird die Anzahl an Backups der `meta.xml`-Datei und der `meta_anchor.xml`-Datei angegeben. **Hinweis:** Wird hier 0 eingetragen, so werden keine Backups gespeichert. |

### Benutzeroberfläche

In der Kategorie "Benutzeroberfläche" sind Einstellungen dokumentiert, mit denen die Darstellung von Inhalten oder die Anzeige/Nicht-Anzeige von Buttons konfiguriert werden kann.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `showOcrButton` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um im Metadateneditor einen Button für das Ausführen der OCR-Analyze am aktuell ausgewählten Strukturelement anzuzeigen. |
| `MetsEditorDisplayFileManipulation` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um im Metadateneditor ungespeicherte geänderte Dokumente anzuzeigen. |
| `MetsEditorShowArchivedFolder` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um archivierte Bilddateien anzuzeigen. |
| `MetsEditorShowMetadataPopup` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um einen Button einzublenden, mit dem weitere Metadaten zu einem Dokument in einem Popup angezeigt werden können. |
| `MetsEditorMaxTitleLength` | Number | `0` | Dieser Wert gibt an, wie viele Zeichen maximal in Namen von Dokumentstrukturelementen angezeigt werden. Ist ein Name länger als der hier angegebene Wert, so werden entsprechend der maximalen Länge nur die ersten Zeichen angezeigt. Dieser Wert kann auf `0` gesetzt werden, um die Maximallänge zu deaktivieren. |

### Bilddateien und Vorschaubilder

In dieser Kategorie sind Einstellungen für Bilddateien, Vorschaubilder, die Darstellung von Bildern und das Tiling (Kachelung) von Bildern in der Benutzeroberfläche dokumentiert.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `ShowImageComments` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um Bildkommentare zu einzelnen Seiten von Dokumenten anzuzeigen. |
| `MetsEditorNumberOfImagesPerPage` | Number | `96` | Dieser Wert gibt an, wie viele Vorschaubilder standardmäßig auf einer Seite im Metadateneditor angezeigt werden. |
| `MetsEditorUseImageTiles` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um Bilddateien auf der Benutzeroberfläche kachelweise (als "Tiles") zu laden. Dies ermöglicht eine flüssigere Darstellung der Bilder. |
| `ImageSorting` | Text | `number` | Dieser Wert gibt an, nach welchem Kriterium Bilddateinamen sortiert werden. Mit dem Wert `number` werden Dateinamen numerisch sortiert (zum Beispiel 1, 10, 30, 100, 200, 1000). Mit dem Wert `alphanumeric` werden Dateinamen lexikographisch sortiert (zum Beispiel 1, 10, 100, 1000, 200, 30). |
| `ImagePrefix` | Text | `\\d{8}` | Dieser Wert kann einen regulären Ausdruck (Regex) beinhalten und gibt an, mit welcher Zeichenfolge Namen von Bilddateien anfangen müssen, um als valide Dateien akzeptiert zu werden. Der Standardpräfix gibt an, dass ein Dateiname mit 8 Ziffern beginnen muss (zB. YYYYMMTT). |
| `UserForImageReading` | Text | `root` | Bilddateien können im nur-lesen-Modus heruntergeladen werden. Diese gehören dann nicht dem Benutzer, sondern einem weiteren virtuellen Nutzer, der die Bilddateien nur mit Leserechten zur Verfügung stellt. Der Benutzername dieses virtuellen Nutzers wird mit diesem Wert konfiguriert. Üblicherweise wird `root` verwendet. |
| `UseImageThumbnails` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um Vorschaubilder von Dokumentseiten anzuzeigen. |
| `MetsEditorThumbnailsize` | Number | `200` | Dieser Wert gibt die Größe in Pixeln an, in der Vorschaubilder im Metadateneditor angezeigt werden. |
| `MaxParallelThumbnailRequests` | Number | `100` | Dieser Wert kann gesetzt werden, um die Anzahl der gleichzeitig geladenen Vorschaubilder zu begrenzen. Diese Option ist insbesondere auf schwächeren Servern sinnvoll. |
| `MetsEditorMaxImageSize` | Number | `15000` | Dieser Wert gibt die maximale Bildgröße in Pixeln an, die ein Bild haben darf, um im Metadateneditor dargestellt zu werden. |

Die maximale Größe von Bilddateien (in Bytes) wird mit zwei unabhängig konfigurierbaren Werten definiert. Mit dem Wert `MaxImageFileSize` wird eine Zahl angegeben, wie zum Beispiel `1`, `5` oder `10`. Mit dem zusätzlichen Wert `MaxImageFileSizeUnit` wird die Maßeinheit angegeben. Diese in Kombination ergeben die Maximale Anzahl an Bytes, die eine Bilddatei nicht überschreiten darf. **Wichtig:** Es können nur ganze Zahlen verwendet werden.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `MaxImageFileSize` | Number | `4000` | Dieser Wert gibt den Faktor für die maximale Bildgröße in Bytes an. |
| `MaxImageFileSizeUnit` | Text | `MB` | Dieser Wert gibt die Maßeinheit an, mit der der Faktor multipliziert wird, um die gesamte Bildgröße in Bytes zu erhalten. |

Da es viele missverständliche Maßeinheiten gibt, sind in der folgenden Tabelle alle akzeptierten Werte und ihre intern verwendeten numerischen Werte angegeben.

| Maßeinheit | Faktor | Bezeichnung |
| ---------- | ------ | ----------- |
| `B` | `1` | Byte |
| `K` oder `KB` | `1000` | Kilobyte |
| `KI` oder `KIB` | `1024` | Kibibyte |
| `M` oder `MB` | `1000*1000` | Megabyte |
| `MI` oder `MIB` | `1024*1024` | Mebibyte |
| `G` oder `GB` | `1000*1000*1000` | Gigabyte |
| `GI` oder `GIB` | `1024*1024*1024` | Gibibyte |
| `T` oder `TB` | `1000*1000*1000*1000` | Terabyte |
| `TI` oder `TIB` | `1024*1024*1024*1024` | Tebibyte |

Damit können zum Beispiel folgende Einstellungen vorgenommen werden:

```ini
# 20 Megabyte -> 20 * 1000 * 1000 = 20 000 000 Byte
MaxImageFileSize=20
MaxImageFileSizeUnit=MB
```

oder

```ini
# 1 Gibibyte -> 1 * 1024 * 1024 * 1024 = 1 073 741 824 Byte
MaxImageFileSize=1
MaxImageFileSizeUnit=GIB
```

Mit den folgenden Werten können Informationen zu unterstützten Bild- und Kachel-Größen (Tile-Größen) für JSON-API-Anfragen konfiguriert werden. Mit der folgenden API-Anfrage können diese Informationen zu Bildern aus Vorgängen abgefragt werden:

```ini
/process/image/{process}/{folder}/{filename}/info.json
```

Dabei können alle Werte mehrfach verwendet werden und mehrere Werte in der API-Anfrage zurückgeben.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `MetsEditorImageSize` | Text | | Mit diesem Wert können mehrere Größen (in Pixel) für allgemeine Bilder angegeben werden. |
| `MetsEditorImageTileSize` | Text | | Mit diesem Wert können mehrere Größen (in Pixel) für Kacheln (Tiles) angegeben werden. |
| `MetsEditorImageTileScale` | Text | | Mit diesem Wert können mehrere Skalierungsgrößen für Kacheln (Tiles) angegeben werden. |

Eine Konfiguration könnte zum Beispiel wie folgt aussehen:

```ini
MetsEditorImageSize=4096

MetsEditorImageTileSize=64
MetsEditorImageTileSize=128
MetsEditorImageTileSize=256

MetsEditorImageTileScale=1
MetsEditorImageTileScale=32
```

Beim Abschließen von Schritten werden verschiedene interne Datenüberprüfungen vorgenommen. Unter anderem wird die Anzahl an vorhandenen und bearbeiteten Bilddateien überprüft. Mit dem Wert `historyImageSuffix` können ein oder mehrere Dateitypen angegeben werden, die für diese Zählung berücksichtigt werden.

Diese Einstellung wird zwar für Dateiendungen verwendet und kann auch allgemeine Texte beinhalten, mit denen ein Dateiname enden soll, es werden allerdings keine regulären Ausdrücke interpretiert.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `historyImageSuffix` | Text | `.tif` | Mit diesem Wert kann ein oder mehrere Dateitypen angegeben werden. |

Sollen zum Beispiel alle `*.tif`, `*.jpg` und `*.jpeg`-Dateien berücksichtigt werden, so könnte folgende Liste zusammengestellt werden:

```ini
historyImageSuffix=.tif
historyImageSuffix=.jpg
historyImageSuffix=.jpeg
```

### Validierung

Diese Kategorie beinhaltet Einstellungen zur Validierung von Vorgängen, Bilddateien und Metadaten.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `useMetadatenvalidierung` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um beim Speichern und Verlassen des Metadateneditor die Metadaten des aktuellen Dokumentes zu validieren. |
| `MetsEditorValidateImages` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um im Metadateneditor einen Validieren-Button anzuzeigen und damit eine durch den Nutzer veranlasste Validierung zu ermöglichen. |
| `validateProcessTitelRegex` | Text | `[\\w-]*` | Dieser Wert gibt einen regulären Ausdruck (Regex) an, der verwendet werden soll, um die Gültigkeit von Vorgangstiteln zu prüfen. |
| `ProcessTitleGenerationRegex` | Text | `[\\W]` | Dieser Wert gibt einen regulären Ausdruck (Regex) an, der verwendet werden soll, um ungültige Sonderzeichen aus Vorgangstiteln zu entfernen. |

### Export

In dieser Kategorie werden Einstellungen beschrieben, die den Export von Vorgängen in herunterladbare oder auf dem Server zwischenspeicherbare Dateien mitbeeinflussen.

| Eigenschaft | Typ | Standardwert | Beschreibung |
| ----------- | --- | ------------ | ------------ |
| `ExportExiftoolPath` | Text | `/usr/bin/exiftool` | Hier werden der Dateipfad und der Programmname des Programms angegeben, das für das Extrahieren von weiteren Metadaten (EXIF-Daten) aus Bilddateien verwendet wird. |
| `useOrigFolder` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um beim Import Bilddateien direkt aus dem master-Ordner zu beziehen. |
| `exportWithoutTimeLimit` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, wenn Exportprozesse keinem Zeitlimit unterliegen sollen. |
| `ExportValidateImages` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um beim Export Bilddateien zu validieren. |
| `ExportMetadataForProject` | Text | | Hier wird der Name eines Metadatenfeldes angegeben, in das der Projektname exportiert werden soll. |
| `ExportMetadataForInstitution` | Text | | Hier wird der Name eines Metadatenfeldes angegeben, in das der Name der Institution exportiert werden soll. |
| `ExportMetadataForDfgViewerUrl` | Text | | Hier wird der Name eines Metadatenfeldes angegeben, in das die URL für den DFG-Viewer exportiert werden soll. |
| `ExportFilesFromOptionalMetsFileGroups` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um optionale Dateigruppen beim Export zu berücksichtigen. |
| `ExportInTemporaryFile` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um Exporte in temporären Dateien zu speichern. |
| `ExportCreateUUID` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um beim Export die UUID (universally unique identifier) von Dateien zu setzen. |
| `ExportCreateTechnicalMetadata` | Boolean | `false` | Dieser Wert kann auf `true` gesetzt werden, um beim Export weitere technische Metadaten bezüglich der Dokumentstruktur zu berücksichtigen. |
| `automaticExportWithImages` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, wenn bei automatischen Exportprozessen Bilddateien mit exportiert werden sollen. |
| `automaticExportWithOcr` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um bei automatischen Exportprozessen eine OCR-Analyse durchzuführen. |
| `pdfAsDownload` | Boolean | `true` | Dieser Wert kann auf `true` gesetzt werden, um exportierte PDF Dokumente zum Download anzubieten. Ist dieser Wert auf `false` gesetzt, so werden exportierte PDF Dokumente im Benutzerordner des entsprechenden Benutzers auf dem Server gespeichert. |