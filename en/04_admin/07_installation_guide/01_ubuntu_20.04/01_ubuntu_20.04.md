# Installation guide - Ubuntu 20.04

## Introduction <a id="einleitung"></a>

The following installation guide for Goobi workflow refers to `Ubuntu Linux 20.04`. It is written as a step-by-step guide from top to bottom, meaning that settings and configurations build on each other. If the order is not followed, certain commands may fail.

The domain name used in this manual is `GOOBI.EXAMPLE.ORG` and should be adapted to your own DNS name.

{% hint style="info" %}
Commands from this manual are best copied by clicking on the corresponding icon. Otherwise there is the danger of copying unwanted whitespaces.
{% endhint %}

## Preparation

We assume that we start with a fresh, up to date `Ubuntu Linux 20.04` installed from the `Server install image` with no additional packages installed. First you have to log on to the server where you want to install Goobi workflow:

```bash
ssh goobi.example.org
```

Passwords must then be generated for the Goobi workflow database and the local LDAP and stored as a session variable:

```bash
export PW_SQL_GOOBI=$(</dev/urandom tr -dc '[:alnum:]' | head -c17)
export PW_LDAP_GOOBI=$(</dev/urandom tr -dc '[:alnum:]' | head -c17)
export NAME_HOST=GOOBI.EXAMPLE.ORG
export BASENAME=dc=GOOBI,dc=EXAMPLE,dc=ORG
export SOURCEDIR=~/goobi/install
export PW_GOOBITESTUSER=$(</dev/urandom tr -dc '[:alnum:]' | head -c17)

install -b -m 600 /dev/null goobi_install_credentials.txt
echo "
### Verwendete Parameter: ###
export PW_SQL_GOOBI=$PW_SQL_GOOBI
export PW_LDAP_GOOBI=$PW_LDAP_GOOBI
export NAME_HOST=$NAME_HOST
export BASENAME=$BASENAME
export SOURCEDIR=$SOURCEDIR
export PW_GOOBITESTUSER=$PW_GOOBITESTUSER 
" | tee goobi_install_credentials.txt
```

## Install packages <a id="pakete-installieren"></a>

Goobi workflow is based on Java, MariaDB, Tomcat and uses Samba and OpenLdap. First we set some pre-configurartion:

```bash
sudo debconf-set-selections << EOF
postfix postfix/main_mailer_type select Local only
postfix postfix/mailname string $NAME_HOST
slapd slapd/internal/adminpw password $PW_LDAP_GOOBI
slapd slapd/password1 password $PW_LDAP_GOOBI
slapd slapd/password2 password $PW_LDAP_GOOBI
slapd shared/organization string $NAME_HOST
slapd slapd/domain string $NAME_HOST
slapd slapd/backend select MDB
nslcd nslcd/ldap-uris string ldap://127.0.0.1/
nslcd nslcd/ldap-base string $BASENAME
libnss-ldapd libnss-ldapd/nsswitch multiselect passwd, group, shadow
EOF
```

Then we start the package installation:

```bash
sudo apt update &&
sudo apt -y install wget curl openjdk-11-jdk-headless tomcat9 mariadb-server apache2 samba smbclient imagemagick graphicsmagick libtiff-tools djvulibre-bin netpbm jhead exiv2 bc unzip git mailutils slapd libnss-ldapd libldap-2.4-2 ldap-utils ldapvi libpam-ldapd smbldap-tools rename poppler-utils
```

Fresh installed services are started right away in Debian like systems, but we do not want the Tomcat server to run yet:

```bash
sudo service tomcat9 stop
```

## Aliases <a id="variablen-und-aliase"></a>

The following aliases should be added to the `/root/.bash_aliases` file:

```bash
cat << "EOF" | sudo tee -a /root/.bash_aliases
alias cata='journalctl -n200 -f -u tomcat9'
alias gl='tail -f -n 333 /opt/digiverso/logs/goobi.log'
EOF
```

## Checkout Goobi from Github

A temporary directory for the installation must be created and the Goobi workflow repository cloned into it. This directory will contain various files that are required for the following installation steps:

```bash
mkdir -p $SOURCEDIR
cd $SOURCEDIR
git clone --depth 1 https://github.com/intranda/goobi-workflow.git
```

It is recommended that you already have a DNS record for the server at this time.

## Configuration of Services <a id="services-konfigurieren"></a>

### LDAP <a id="ldap"></a>

#### Configuration of the LDAP-Server

First the LDAP should be responsible only for `localhost`. For this the setting of the `SLAPD_SERVICES` must be modified in the file `/etc/default/slapd`:

```bash
sudo patch /etc/default/slapd << "EOF"
@@ -21,7 +21,7 @@
 # sockets.
 # Example usage:
 # SLAPD_SERVICES="ldap://127.0.0.1:389/ ldaps:/// ldapi:///"
-SLAPD_SERVICES="ldap:/// ldapi:///"
+SLAPD_SERVICES="ldap://127.0.0.1:389/ ldapi:///"

 # If SLAPD_NO_START is set, the init script will not start or restart
 # slapd (but stop will still work).  Uncomment this if you are
EOF
```

Then the following step is executed:

```bash
cat /usr/share/doc/samba/examples/LDAP/samba.schema | sudo tee /etc/ldap/schema/samba.schema
```

The file `samba.ldif` can then be moved to the path `/etc/ldap/schema/` and the schema inserted into the LDAP:

```bash
sudo cp $SOURCEDIR/goobi-workflow/install/ldap/samba.ldif /etc/ldap/schema/
sudo ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/samba.ldif
```

We create OUs and the cn=NextFreeUnixId for Goobi:

```bash
ldapadd -x -D cn=admin,$BASENAME -w "$PW_LDAP_GOOBI" -f <(sed -e"s|dc=GOOBI,dc=EXAMPLE,dc=ORG|$BASENAME|" $SOURCEDIR/goobi-workflow/install/ldap/import.ldif)
```

The `/etc/ldap/ldap.conf` file is then modified as follows:

```bash
cat << EOF | sudo tee /etc/ldap/ldap.conf
#
# LDAP Defaults
#

BASE         $BASENAME
URI          ldap://127.0.0.1
TLS_REQCERT  never
EOF
```

```bash
sudo ldapmodify -Y EXTERNAL -H ldapi:/// -f $SOURCEDIR/goobi-workflow/install/ldap/index.ldif
```

#### Using the tool ldapvi

`ldapvi` is a good tool for later, easier editing of values in LDAP. For this the following entries in the file `/etc/ldapvi.conf` have to be adapted and inserted:

```bash
sudo chmod 600 /etc/ldapvi.conf
echo "user: cn=admin,$BASENAME" | sudo tee -a /etc/ldapvi.conf
echo "password: $PW_LDAP_GOOBI" | sudo tee -a /etc/ldapvi.conf
```

### Setting up Samba <a id="samba"></a>

The Samba server is connected to the LDAP. The configuration file must be replaced with the one from the repository and then the LDAP configuration must be adapted:

```bash
sed -e"s|dc=GOOBI,dc=EXAMPLE,dc=ORG|$BASENAME|" $SOURCEDIR/goobi-workflow/install/samba/smb.conf | sudo tee /etc/samba/smb.conf
```

Samba needs the password for the LDAP Admin for this:

```bash
sudo smbpasswd -w "$PW_LDAP_GOOBI"
```

{% hint style="info" %}
Samba does not distinguish between upper and lower case for user names!
{% endhint %}

```bash
sudo systemctl restart smbd
```

#### Samba: Free memory display <a id="samba-anzeige-freier-speicher"></a>

The upload of the images usually takes place within the directory path `/opt/digiverso`. Therefore Samba should also display the free memory from there.:

```bash
sudo cp "$SOURCEDIR/goobi-workflow/install/samba/samba-dfree" /usr/local/bin/samba-dfree
sudo chmod 755 /usr/local/bin/samba-dfree
```

### Setting up the database MySQL / MariaDB <a id="mysql-mariadb"></a>

Goobi workflow requires a database and its own user. The following command also imports the database schema and creates an initial structure:

```bash
sudo mysql -e "CREATE DATABASE goobi;
USE goobi;
SOURCE $SOURCEDIR/goobi-workflow/install/db/goobi_blank.sql;
CREATE USER 'goobi'@'localhost' IDENTIFIED BY '$PW_SQL_GOOBI';
GRANT ALL PRIVILEGES ON goobi.* TO 'goobi'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;"
```

### Setting up the Tomcat server <a id="tomcat"></a>

In the file `/etc/default/tomcat9` the memory under `-Xmx` should be adapted to the available machine memory. The garbage collector options to be used are also selected and `urandom` configured for a faster Tomcat start:

```bash
sudo patch /etc/default/tomcat9 << "EOF"
@@ -5,7 +5,16 @@
 
 # You may pass JVM startup parameters to Java here. If unset, the default
 # options will be: -Djava.awt.headless=true -XX:+UseG1GC
-JAVA_OPTS="-Djava.awt.headless=true -XX:+UseG1GC"
+JAVA_OPTS="-Djava.awt.headless=true -Xmx2g -Xms2g"
+JAVA_OPTS="${JAVA_OPTS} -XX:+UseG1GC"
+JAVA_OPTS="${JAVA_OPTS} -XX:+ParallelRefProcEnabled"
+JAVA_OPTS="${JAVA_OPTS} -XX:+DisableExplicitGC"
+JAVA_OPTS="${JAVA_OPTS} -XX:+CMSClassUnloadingEnabled"
+JAVA_OPTS="${JAVA_OPTS} -Djava.security.egd=file:/dev/./urandom"
+JAVA_OPTS="${JAVA_OPTS} -Dlog4j2.formatMsgNoLookups=true"
+JAVA_OPTS="${JAVA_OPTS} -Dfile.encoding='utf-8'"
+
+export UMASK=0022
 
 # To enable remote debugging uncomment the following line.
 # You will then be able to use a Java debugger on port 8000.
@@ -19,4 +28,4 @@
 #SECURITY_MANAGER=true
 
 # Whether to compress logfiles older than today's
-#LOGFILE_COMPRESS=1
+LOGFILE_COMPRESS=1
EOF
```

In the file `/etc/tomcat9/server.xml` the Tomcat is configured to listen only on `localhost`, appropriate connectors are set up for the proxy:

```bash
sed -e "s/GOOBI_HOSTNAME/$NAME_HOST/" << "EOF" | sudo patch /etc/tomcat9/server.xml
@@ -67,54 +67,18 @@
          Define a non-SSL/TLS HTTP/1.1 Connector on port 8080
     -->
-    <Connector port="8080" protocol="HTTP/1.1"
-               connectionTimeout="20000"
-               redirectPort="8443" />
-    <!-- A "Connector" using the shared thread pool-->
-    <!--
-    <Connector executor="tomcatThreadPool"
-               port="8080" protocol="HTTP/1.1"
-               connectionTimeout="20000"
-               redirectPort="8443" />
-    -->
-    <!-- Define a SSL/TLS HTTP/1.1 Connector on port 8443
-         This connector uses the NIO implementation. The default
-         SSLImplementation will depend on the presence of the APR/native
-         library and the useOpenSSL attribute of the
-         AprLifecycleListener.
-         Either JSSE or OpenSSL style configuration may be used regardless of
-         the SSLImplementation selected. JSSE style configuration is used below.
-    -->
-    <!--
-    <Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
-               maxThreads="150" SSLEnabled="true">
-        <SSLHostConfig>
-            <Certificate certificateKeystoreFile="conf/localhost-rsa.jks"
-                         type="RSA" />
-        </SSLHostConfig>
-    </Connector>
-    -->
-    <!-- Define a SSL/TLS HTTP/1.1 Connector on port 8443 with HTTP/2
-         This connector uses the APR/native implementation which always uses
-         OpenSSL for TLS.
-         Either JSSE or OpenSSL style configuration may be used. OpenSSL style
-         configuration is used below.
-    -->
-    <!--
-    <Connector port="8443" protocol="org.apache.coyote.http11.Http11AprProtocol"
-               maxThreads="150" SSLEnabled="true" >
-        <UpgradeProtocol className="org.apache.coyote.http2.Http2Protocol" />
-        <SSLHostConfig>
-            <Certificate certificateKeyFile="conf/localhost-rsa-key.pem"
-                         certificateFile="conf/localhost-rsa-cert.pem"
-                         certificateChainFile="conf/localhost-rsa-chain.pem"
-                         type="RSA" />
-        </SSLHostConfig>
-    </Connector>
-    -->
+    <Connector address="127.0.0.1" port="8080" protocol="HTTP/1.1"
+                   maxThreads="400"
+                   URIEncoding="UTF-8"
+                   enableLookups="false"
+                   disableUploadTimeout="true"
+                   proxyName="GOOBI_HOSTNAME"
+                   proxyPort="80" />

     <!-- Define an AJP 1.3 Connector on port 8009 -->
-    <!--
-    <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
-    -->
+       <Connector address="127.0.0.1" port="8009" protocol="AJP/1.3"
+                secretRequired="false"
+                connectionTimeout="20000"
+                maxThreads="400"
+                URIEncoding="UTF-8" />


@@ -160,7 +124,12 @@
              Documentation at: /docs/config/valve.html
              Note: The pattern used is equivalent to using pattern="common" -->
+   <!--
         <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
                prefix="localhost_access_log" suffix=".txt"
                pattern="%h %l %u %t &quot;%r&quot; %s %b" />
+   -->
+       <Valve className="org.apache.catalina.valves.CrawlerSessionManagerValve"
+              crawlerUserAgents=".*[bB]ot.*|.*Yahoo! Slurp.*|.*Feedfetcher-Google.*|.*Apache-HttpClient.*|.*[Ss]pider.*|.*[Cc]rawler.*|.*nagios.*|.*Yandex.*"
+              sessionInactiveInterval="60"/>

       </Host>
EOF
```

Then the session persistence within the file `/etc/tomcat9/context.xml` is deactivated by commenting the following line:

```bash
sudo patch /etc/tomcat9/context.xml << "EOF"
@@ -25,7 +25,5 @@
     <WatchedResource>${catalina.base}/conf/web.xml</WatchedResource>

     <!-- Uncomment this to disable session persistence across Tomcat restarts -->
-    <!--
     <Manager pathname="" />
-    -->
 </Context>
EOF
```

Tomcat needs more rights:

```bash
sudo SYSTEMD_EDITOR=tee systemctl edit tomcat9 << "EOF"
[Service]
LogsDirectoryMode=755
CacheDirectoryMode=755
ProtectSystem=true
NoNewPrivileges=false
ReadWritePaths=
EOF
sudo systemctl daemon-reload
```

### Configuration of Apache <a id="apache"></a>

The Apache web server must be set up to make Goobi workflow available externally. The following modules are activated for this purpose:

```bash
sudo a2enmod proxy_ajp
sudo a2enmod proxy_wstunnel
sudo a2enmod rewrite
sudo a2enmod headers
```

The following file must be saved as `/etc/apache2/sites-available/GOOBI.EXAMPLE.ORG.conf`:

```bash
sed -e "s/GOOBI.EXAMPLE.ORG/$NAME_HOST/" << "EOF" | sudo tee /etc/apache2/sites-available/$NAME_HOST.conf
<VirtualHost *:80>
        ServerAdmin support@intranda.com
        ServerName GOOBI.EXAMPLE.ORG
        DocumentRoot /var/www

        RequestHeader unset Expect early

        ## compress output
        <IfModule mod_deflate.c>
                AddOutputFilterByType DEFLATE text/plain text/html text/xml
                AddOutputFilterByType DEFLATE text/css text/javascript
                AddOutputFilterByType DEFLATE application/xml application/xhtml+xml
                AddOutputFilterByType DEFLATE application/rss+xml
                AddOutputFilterByType DEFLATE application/javascript application/x-javascript
        </IfModule>

        ## make sure rewrite is enabled
        RewriteEngine On

        ## Enable WebSockets
        RewriteCond %{HTTP:Upgrade} websocket [NC]
        RewriteCond %{HTTP:Connection} upgrade [NC]
        RewriteRule /?(.*) ws://localhost:8080/$1 [P,L]

        ## general proxy settings
        ProxyPreserveHost On
        ProxyVia On
        <Proxy *>
                Require local
        </Proxy>

        ## goobi
        redirect /index.html http://GOOBI.EXAMPLE.ORG/goobi/
        redirectmatch /goobi$ http://GOOBI.EXAMPLE.ORG/goobi/

        <Location "/goobi/">
                Require all granted
                ProxyPass ajp://localhost:8009/goobi/ retry=0
                ProxyPassReverse ajp://localhost:8009/goobi/
        </Location>

        ## disable external connection to Goobi WebAPI globally
        # ProxyPass /goobi/wi !

        ## only allow access to Goobi WebAPI for certain hosts
        <Location "/goobi/wi">
                # Require ip 1.2.3.4
                Require local
        </Location>

        ## logging
        CustomLog /var/log/apache2/GOOBI.EXAMPLE.ORG_access.log combined
        ErrorLog /var/log/apache2/GOOBI.EXAMPLE.ORG_error.log

        # Possible values include: debug, info, notice, warn, error, crit, alert, emerg.
        LogLevel warn
</VirtualHost>
EOF
```

The Goobi workflow `vhost` is now activated, the default `vhost` is deactivated and the Apache web server is restarted:

```bash
sudo a2dissite 000-default.conf
sudo a2ensite $NAME_HOST.conf
sudo systemctl restart apache2
```

### Setting up sudo <a id="sudo"></a>

Goobi workflow requires different rights to execute scripts. The following file for the sudo rights must be stored for this:

```bash
cat << "EOF" | sudo EDITOR='tee' visudo -f /etc/sudoers.d/70_goobi
##
# Goobi sudoers file
##

# Berechtigungen fuer Tomcat Server
User_Alias HTTPD=tomcat

# In den Shellscripten definierte Kommandos:
# script_chownTomcat.sh, script_chownUser.sh, script_createDirUserHome.sh,
# script_createSymLink.sh
Cmnd_Alias CHOWN_DATEN=/bin/chown * /opt/digiverso/goobi/metadata/*

# script_createDirUserHome.sh
Cmnd_Alias CHGRP_USERS=/bin/chgrp tomcat /home/*
Cmnd_Alias CHMOD_USERS=/bin/chmod g+w /home/*
Cmnd_Alias CHMOD_WRITE=/bin/chmod * /opt/digiverso/goobi/metadata/*
Cmnd_Alias CHOWN_USERS=/bin/chown * /home/*
Cmnd_Alias MKDIR_USERS=/bin/mkdir /home/*

# Der Tomcat Server darf die in den Shellscripten definierten Kommandos ohne
# Passwortabfrage mit root Berechtigung ausfuehren
HTTPD ALL=NOPASSWD: CHOWN_DATEN, CHGRP_USERS, CHMOD_USERS, CHOWN_USERS, MKDIR_USERS, CHMOD_WRITE

HTTPD ALL=NOPASSWD: /bin/mount --bind /opt/digiverso/goobi/metadata/* /home/*
HTTPD ALL=NOPASSWD: /bin/umount -l /home/*
HTTPD ALL=NOPASSWD: /bin/rmdir /home/*
HTTPD ALL=NOPASSWD: /bin/chmod * /home/*
EOF
```

## Creation of the directory structure <a id="verzeichnisstruktur-erstellen"></a>

The following commands create the necessary folder structure and move the files from the repository to the expected location:

```bash
sudo mkdir -p /opt/digiverso/{logs,viewer/hotfolder,goobi/{activemq,config,lib,metadata,rulesets,scripts,static_assets,tmp,xslt,plugins/{administration,command,dashboard,export,GUI,import,metadata,opac,statistics,step,validation,workflow}}}
sudo cp $SOURCEDIR/goobi-workflow/install/config/* /opt/digiverso/goobi/config/
sudo cp $SOURCEDIR/goobi-workflow/install/scripts/* /opt/digiverso/goobi/scripts/
sudo cp $SOURCEDIR/goobi-workflow/install/rulesets/* /opt/digiverso/goobi/rulesets/
sudo cp $SOURCEDIR/goobi-workflow/install/xslt/* /opt/digiverso/goobi/xslt/
sudo chown -R tomcat: /opt/digiverso/*
```

## Deployment of Goobi workflow

The following file has to be stored under the path `/etc/tomcat9/Catalina/localhost/goobi.xml`:

```bash
sed -e "s/PW_SQL_GOOBI/$PW_SQL_GOOBI/" << "EOF" | sudo tee /etc/tomcat9/Catalina/localhost/goobi.xml
<?xml version='1.0' encoding='utf-8'?>
<Context>
        <Manager className="org.apache.catalina.session.PersistentManager" saveOnRestart="false">
                <Store className="org.apache.catalina.session.FileStore"/>
        </Manager>

        <Resources>
                <PreResources
                  className="org.apache.catalina.webresources.DirResourceSet"
                  base="/opt/digiverso/goobi/plugins/GUI/"
                  webAppMount="/WEB-INF/lib" />

                <PostResources
                  className="org.apache.catalina.webresources.DirResourceSet"
                  base="/opt/digiverso/goobi/lib/"
                  webAppMount="/WEB-INF/lib" />
        </Resources>


<Resource name="goobi"
          auth="Container"

          factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
          type="javax.sql.DataSource"

          driverClassName="software.aws.rds.jdbc.mysql.Driver"
          username="goobi"
          password="PW_SQL_GOOBI"
          maxActive="100"
          maxIdle="30"
          minIdle="4"
          maxWait="10000"
          testOnBorrow="true"
          testWhileIdle="true"
          validationQuery="SELECT SQL_NO_CACHE 1"
          removeAbandoned="true"
          removeAbandonedTimeout="600"
          url="jdbc:mysql://localhost/goobi?characterEncoding=UTF-8&amp;autoReconnect=true&amp;autoReconnectForPools=true" />

</Context>
EOF
```

Now the file permissions are adjusted so that the file is not deleted accidental during an update:

```bash
sudo chown -R root:tomcat /etc/tomcat9/Catalina
sudo chmod -R g-w /etc/tomcat9/Catalina
```

In the following, Goobi workflow is downloaded and moved to the expected location in the file system:

```bash
wget https://github.com/intranda/goobi-workflow/releases/latest/download/goobi.war -O - | sudo tee /var/lib/tomcat9/webapps/goobi.war >/dev/null
```

## Deployment of Plugins <a id="deployment-von-plugins"></a>

Some plugins have to be downloaded to the expected location in the file system for commissioning:

```bash
# Temporary rights:
sudo chown -R ${USER}: /opt/digiverso/goobi/{lib,plugins,config}

wget -cP /opt/digiverso/goobi/plugins/opac/ "https://github.com/intranda/goobi-plugin-opac-pica/releases/latest/download/plugin-opac-pica-base.jar"
wget -cP /opt/digiverso/goobi/plugins/opac/ "https://github.com/intranda/goobi-plugin-opac-marc/releases/latest/download/plugin-opac-marc-base.jar"

# Step: Fileupload
wget -cP /opt/digiverso/goobi/plugins/GUI/  "https://github.com/intranda/goobi-plugin-step-file-upload/releases/latest/download/plugin-step-file-upload-gui.jar"
wget -cP /opt/digiverso/goobi/plugins/step/ "https://github.com/intranda/goobi-plugin-step-file-upload/releases/latest/download/plugin-step-file-upload-base.jar"
wget -cP /opt/digiverso/goobi/config/       "https://github.com/intranda/goobi-plugin-step-file-upload/releases/latest/download/plugin_intranda_step_fileUpload.xml"

# Step: ImageQA
wget -cP /opt/digiverso/goobi/plugins/GUI/  "https://github.com/intranda/goobi-plugin-step-imageqa/releases/latest/download/plugin-step-imageqa-gui.jar"
wget -cP /opt/digiverso/goobi/plugins/step/ "https://github.com/intranda/goobi-plugin-step-imageqa/releases/latest/download/plugin-step-imageqa-base.jar"
wget -cP /opt/digiverso/goobi/config/       "https://github.com/intranda/goobi-plugin-step-imageqa/releases/latest/download/plugin_intranda_step_imageQA.xml"

# Dashboard: Extended
wget -cP /opt/digiverso/goobi/plugins/GUI/       "https://github.com/intranda/goobi-plugin-dashboard-extended/releases/latest/download/plugin-dashboard-extended-gui.jar"
wget -cP /opt/digiverso/goobi/plugins/dashboard/ "https://github.com/intranda/goobi-plugin-dashboard-extended/releases/latest/download/plugin-dashboard-extended-base.jar"
wget -cP /opt/digiverso/goobi/config/            "https://github.com/intranda/goobi-plugin-dashboard-extended/releases/latest/download/plugin_intranda_dashboard_extended.xml"

# REST: intranda REST
wget -cP /opt/digiverso/goobi/lib/ "https://github.com/intranda/goobi-plugin-rest-intranda/releases/latest/download/plugin-rest-intranda-api.jar"

# Controlling: intranda default statistics
wget -cP /opt/digiverso/goobi/plugins/GUI/        "https://github.com/intranda/goobi-plugin-statistics-intranda/releases/latest/download/plugin-statistics-intranda-gui.jar"
wget -cP /opt/digiverso/goobi/plugins/statistics/ "https://github.com/intranda/goobi-plugin-statistics-intranda/releases/latest/download/plugin-statistics-intranda-base.jar"
wget -cP /opt/digiverso/goobi/plugins/statistics/ "https://github.com/intranda/goobi-plugin-statistics-intranda/releases/latest/download/statistics_template.pdf"
wget -cP /opt/digiverso/goobi/plugins/statistics/ "https://github.com/intranda/goobi-plugin-statistics-intranda/releases/latest/download/statistics_template.xlsx"

sudo chown -R tomcat: /opt/digiverso/goobi/{lib,plugins,config}
```

The Tomcat service can then be restarted:

```bash
sudo systemctl restart tomcat9
```

## Configuration and Settings <a id="goobi-einstellungen"></a>

### Creating Users in LDAP <a id="benutzer-ins-ldap-schreiben-und-intrandasupport-account-anlegen"></a>

The test accounts must be written to the LDAP. Please note that `dn`, `sambaPrimaryGroupSID` and `sambaSID` are adapted in the file `testuser.ldif`:

```bash
SID=$(sudo net getlocalsid | awk '{print $NF}')
NLTMHASH_PW_GOOBITESTUSER=$(python3 -c "import hashlib; pw = '$PW_GOOBITESTUSER'; print(hashlib.new('md4', pw.encode('utf-16le')).hexdigest().upper());")
SLAPHASH_PW_GOOBITESTUSER=$(slappasswd -s "$PW_GOOBITESTUSER")
sudo bash -c "
ldapadd -x -D cn=admin,$BASENAME -w $PW_LDAP_GOOBI -f <(sed \
-e's|S-1-5-21-531335965-4077168823-1713822973|$SID|' \
-e's|dc=GOOBI,dc=EXAMPLE,dc=ORG|$BASENAME|' \
-e's|sambaNTPassword: 0CB6948805F797BF2A82807973B89537|sambaNTPassword: $NLTMHASH_PW_GOOBITESTUSER|' \
-e's|userPassword:: e1NTSEF9ZWtKaFpTZklJcndHdjlKTU1rYmxmOUwvZGQ3S3pmU1Y=|userPassword: $SLAPHASH_PW_GOOBITESTUSER|' \
$SOURCEDIR/goobi-workflow/install/ldap/testuser.ldif)
"
sudo service nscd restart
sudo nscd -i passwd
```

The home directories for the users are created, but first ensure that the users are known to the system:

```bash
id testadmin
```

When the user testadmin is found, go on with the home directory creation:

```bash
cd /home &&
for i in testadmin testscanning testmetadata testimaging testqc testprojectmanagement ; do
  sudo mkdir $i
  sudo chown $i:tomcat $i
  sudo chmod 775 $i
done
cd -
```

In addition, the `SID` for Goobi workflow is changed, the value for `userDN` is adjusted, we use the just installed local LDAP and remove an unused user:

```bash
sudo mysql goobi -e "update ldapgruppen
  set
    sambaSID='$SID-{uidnumber*2+1000}',
    sambaPrimaryGroupSID='$SID-100',
    userDN='cn={login},ou=users,ou=goobi,$BASENAME',
    adminLogin='cn=admin,$BASENAME',
    adminPassword='$PW_LDAP_GOOBI',
    ldapUrl='ldap://localhost:389/',
    nextFreeUnixId='cn=NextFreeUnixId,$BASENAME',
    encryptionType='SHA',
    useSsl=0,
    authenticationType='ldap',
    readonly=0,
    readDirectoryAnonymous=0,
    useLocalDirectoryConfiguration=0,
    ldapHomeDirectoryAttributeName='homeDirectory',
    useTLS=0
  where ldapgruppenID=2;"
sudo mysql goobi -e "delete from benutzer where login='goobi';"
```

A test of the SMB access can be performed as follows:

```bash
smbclient -U testadmin%$PW_GOOBITESTUSER //localhost/testadmin -c dir
```

### First login

With the account `testadmin` and the given password `$PW_GOOBITESTUSER` it is now possible to log in. The application runs here: [http://$NAME_HOST/goobi/uii/index.xhtml](http://$NAME_HOST/goobi/uii/index.xhtml)

#### Troubleshooting

* Check the logs:
  * `sudo journalctl -eu tomcat9.service`
  * `less /opt/digiverso/logs/goobi.log`
* Is Tomcat running?
  * `ps aux | grep tomcat`
  * `sudo systemctl status tomcat9.service`
* Is MariaDB running? Is there a database "goobi"?
  * `ps aux | grep -e mysql -e maria`
  * `sudo mysqlshow goobi`
* Is Apache httpd running? Is the "goobi" vhost enabled?
* Are you able to access Goobi workflow on the server's command line?
  * Accessing Apache httpd: `curl http://localhost/goobi/uii/index.xhtml`
  * Accessing Tomcat directly: `curl http://localhost:8080/goobi/uii/index.xhtml`
* Check the network configuration and the hostname / DNS name of the server. Especially when you are running this installation as a first test in a VirtualBox environment, the accessibility depends on the VirtualBox Network Adapter settings, and DNS names might not work. In this case try: [http://$IP/goobi/uii/index.xhtml](http://$IP/goobi/uii/index.xhtml)

### Further configuration

#### Configuration file**: goobi_opac.xml** <a id="goobi_opac-xml"></a>

In the file `goobi_opac.xml` the used catalog can be entered or adapted:

{% code title="/opt/digiverso/goobi/config/goobi_opac.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<opacCatalogues>
    [...]
    <catalogue title="K10Plus">
        <config address="kxp.k10plus.de" database="2.1" description="K10plus" iktlist="IKTLIST-GBV.xml" port="80" ucnf="UCNF=NFC&amp;XPNOFF=1" />
    </catalogue>
</opacCatalogues>
```
{% endcode %}

#### Configuration file**: goobi_projects.xml** <a id="goobi_projects-xml"></a>

In the configuration file `goobi_projects.xml` several important parameters for the creation of processes are defined. Among other things, this concerns the institution name, the current year or also the catalog used by default:

{% code title="/opt/digiverso/goobi/config/goobi_projects.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<goobiProjects>
    <project name="default">
        <createNewProcess>
            <itemlist>
                <item from="werk" multiselect="true">
                    Creator of digital edition
                    <select label="Library of Congress (LoC)">Library of Congress</select>
                </item>
                [...]
                <item docstruct="topstruct" isnotdoctype="periodical|multivolume" metadata="_dateDigitization" multiselect="true" required="true" ughbinding="true">
                    Digitisation date
                    <select label="2021">2021</select>
                </item>
                [...]
            </itemlist>
            <opac use="true">
                <catalogue>Library of Congress</catalogue>
            </opac>
        </createNewProcess>
    </project>
</goobiProjects>
```
{% endcode %}

#### Configuration file**: goobi_digitalCollections.xml** <a id="goobi_digitalcollections-xml"></a>

In the configuration file `goobi_digitalCollections.xml` different collections can be adapted for the created example project. As an example this could look like this:

{% code title="/opt/digiverso/goobi/config/goobi_digitalCollections.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<DigitalCollections>
    <default>
        <DigitalCollection>DefaultCollection</DigitalCollection>
    </default>

    <project>
        <name>sample_project</name>
        <DigitalCollection>Monograph</DigitalCollection>
        <DigitalCollection>Varia</DigitalCollection>
    </project>
</DigitalCollections>
```
{% endcode %}

#### Goobi viewer integration - prepare NFS share

Setting up NFS is only relevant if the Goobi viewer is also installed or is to be installed, and this installation is not performed on the same machine.

In this case, the `/opt/digiverso/viewer` folder must be exported from the Goobi viewer server and mounted in the Goobi workflow server. The adjustments for this are as follows:

```bash
export IP_VIEWER=1.2.3.4   # IP-Adresse of the Goobi viewer server
sudo apt install -y nfs-common
sudo mkdir /opt/digiverso/viewer/hotfolder -p
sudo chown root:root /opt/digiverso/viewer/hotfolder
echo "${IP_VIEWER}:/opt/digiverso/viewer/hotfolder    /opt/digiverso/viewer/hotfolder   nfs     rsize=8192,wsize=8192,soft,intr,rw,nolock,auto,x-systemd.automount 0  0" | sudo tee -a /etc/fstab
```

### Optional: Track changes using Git

For a better traceability of changes to plugins, configuration, scripts, rulesets and XSLTs, you can (optionally) create a local Git repository:

```bash
cat > /opt/digiverso/goobi/.gitignore << "EOF"
.*~
*~
/metadata
/activemq
/tmp
*backup*
EOF

cat > /etc/cron.d/intranda-autocommit-git-goobi-config << "EOF"
MAILTO=root
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

1 0 * * *  root  /bin/bash -c "cd /opt/digiverso/goobi && git add -A && git commit -a -m cron\ auto\ commit" >/dev/null
EOF

git -C /opt/digiverso/goobi init
git -C /opt/digiverso/goobi add -A
git -C /opt/digiverso/goobi commit -a -m 'initial commit'
```