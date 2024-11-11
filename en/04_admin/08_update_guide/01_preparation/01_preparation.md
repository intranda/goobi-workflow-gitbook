# Preparation of an update

## General information

When you update Goobi workflow, all plug-ins should also be updated. You should also check the page `Installed plug-ins` in Goobi workflow. If this page does not yet exist, the relevant files must be identified in the file system. It is important not to forget the REST API.

{% hint style="info" %}
Commands from this manual are best copied by clicking on the corresponding icon. Otherwise there is the danger of copying unwanted whitespaces.
{% endhint %}

## Sensible preparatory work before carrying out the update

### Checking the condition

To ensure the machine is in good condition, the following items should be checked before and/or after the update:

* [ ] Check configuration files for XML errors:

```bash
find /opt/digiverso/goobi/{rulesets,config} /opt/digiverso/itm/{config,templates} /etc/tomcat9  -name "*.xml" -exec xmllint --noout {} \;
```

* [ ] It may happen that the database contains user accounts without authentication type. These can be determined with the following SQL statement for correction. If the command outputs something, the corresponding users must be searched for in the database table and corrected:

```bash
mysql goobi -e'SELECT DISTINCT ldapgruppenid FROM benutzer WHERE ldapgruppenid NOT IN (SELECT ldapgruppenid FROM ldapgruppen) OR ldapgruppenid IS NULL'
```

* [ ] For all database tables, Goobi workflow uses `InnoDB`:

```bash
mysql goobi -NBse 'SELECT table_name FROM INFORMATION_SCHEMA.TABLES where TABLE_SCHEMA="goobi" and TABLE_TYPE="BASE TABLE" and ENGINE != "InnoDB"' | while read i; do echo $i; mysql goobi -e "alter table $i ENGINE = InnoDB"; done
```

* [ ] **goobi_opac.xml**: For multi-volume works the `rulesetChildType` must be set ([template](https://github.com/intranda/goobi-workflow/blob/master/Goobi/install/config/goobi_opac.xml#L36)).
* [ ] **goobi_projects.xml**: No more BoundBook may appear ([template](https://github.com/intranda/goobi-workflow/blob/master/Goobi/install/config/goobi_projects.xml)).

### Creation of a backup

It makes sense to issue the Tomcat before the backup. However, it is necessary to check beforehand that no other user is logged into Goobi workflow. In addition to displaying the users who are logged in in the interface, the last entries in the process log or the last logins can be helpful in assessing the situation:

```bash
mysql goobi -e'select creationDate, userName, type, left(content,70) from journal order by creationDate desc limit 30'
grep user\ DN /opt/digiverso/logs/goobi.log -B1 | tail
# active users, needs /currentusers configured in goobi_rest.xml
PW=$(xmlstarlet sel -t -v '//endpoint[@path="/currentusers"]//allow[1]/@token' -n /opt/digiverso/goobi/config/goobi_rest.xml) && curl -X GET -H "token: $PW" localhost:8080/goobi/api/currentusers -s | jq
```

The Tomcat process for Goobi workflow can then be terminated:

```bash
systemctl stop tomcat9
```

Use the following commands to create a backup directory and copy the files to it:

```bash
BAK=/home/intranda/BACKUP/$(date -I) && mkdir $BAK -p
mysqldump goobi | gzip > $BAK/goobi.$(date +%s).sql.gz
mkdir $BAK/goobi $BAK/webapps
cp -at $BAK/goobi /opt/digiverso/goobi/{config,lib,plugins,rulesets,scripts,static_assets,xslt}
cp -at $BAK/webapps /var/lib/tomcat9/webapps/goobi
# If intranda TaskManager is installed
cp -at $BAK/webapps /var/lib/tomcat9/webapps/itm
cp -at $BAK/ /opt/digiverso/itm
# If LayoutWizzard is installed
cp -at $BAK /opt/digiverso/[L,l]ayout[w,W]izzard
```

Commit the current state in the Goobi folder:

```bash
git -C /opt/digiverso/goobi/ add -A ; git -C /opt/digiverso/goobi/ commit -a -m 'pre update'
```

Save the current status of the archives:

If an update is performed from a version lower than 24.07 to the current version, all EAD files must be exported from BaseX. To do this, log in at `https://URL/basex/dba/login`. Then select each database under `Databases`, select the .xml file and download it.

### Copy the new files to this machine

It is recommended to copy the files to /tmp/g3 on the machine to be updated. Move the files to the correct paths:

```bash
U=/tmp/g3
G=/opt/digiverso/goobi

mv ${U:-/tmp/g3}/goobi.war /var/lib/tomcat9/webapps/

# find ${G:-/opt/digiverso/goobi}/{lib,plugins} -name 'plugin*jar' -delete

mv ${U:-/tmp/g3}/statistics_template.* ${G:-/opt/digiverso/goobi}/plugins/statistics/
mv ${U:-/tmp/g3}/plugin*-gui.jar ${G:-/opt/digiverso/goobi}/plugins/GUI/
mv ${U:-/tmp/g3}/plugin*-lib.jar ${G:-/opt/digiverso/goobi}/lib/
mv ${U:-/tmp/g3}/plugin*-api.jar ${G:-/opt/digiverso/goobi}/lib/
mv ${U:-/tmp/g3}/plugin*-job.jar ${G:-/opt/digiverso/goobi}/lib/

find ${U:-/tmp/g3} -name 'plugin-*-base.jar' -printf '%f\n' | awk -F'-' '{print $0"\t"$2}' | while read -r file type; do
    mv "/tmp/g3/${file}" "${G:-/opt/digiverso/goobi}/plugins/${type}/"
done

# If intranda TaskManager is installed
mv ${U:-/tmp/g3}/itm.war /var/lib/tomcat9/webapps/
mv ${U:-/tmp/g3}/TaskClient.jar /opt/digiverso/itm/bin/TaskClient.jar

# If LayoutWizzard is installed
cp -p ${U:-/tmp/g3}/LayoutWizzard-jar-with-dependencies.jar ${G:-/opt/digiverso/goobi}/lib/
cp -p ${U:-/tmp/g3}/LayoutWizzard-jar-with-dependencies.jar /opt/digiverso/itm/lib/
```

{% hint style="info" %}
Especially configuration files of plugins can have a different file name due to a change in the naming scheme.
{% endhint %}

When the work is complete, the timestamp comparison can be used to determine whether all necessary files have been updated:

```bash
ls -lh /opt/digiverso/goobi/plugins/*/*
ls -lh /opt/digiverso/goobi/lib/*
```

Plugins that are built as `tar` package:

```bash
goobiInstallPlugin() {
    tar -C /opt/digiverso/goobi/ -xvf $1 --exclude "pom.xml"
}
# Example:
goobiInstallPlugin /tmp/g3/plugin_intranda_step_replace-images.tar
```

### Testing the installed update

The following things should be checked after an update:

* [ ] Acceptance and submission of tasks, in particular linking (if necessary mounting) the image folder to the home directory
* [ ] Image display in ImageQA plugin
* [ ] Image and thumbnail display in the metadata editor
* [ ] Image display in the LayoutWizzard plugin
* [ ] Generation of dockets
* [ ] Transfer of jobs to the intranda TaskManager and a message in the process log when a job in the TaskManager is cancelled (if there are changes to the communication between Goobi workflow and the TaskManager)
* [ ] Catalogue queries
* [ ] All plugins are up to date in: Administration -> Installed plugins

### Rescue in case of problems

Sometimes errors may occur after the update. The following points help to identify and solve typical problems:

#### Goobi does not start - ActiveMQ

If the Tomcat hangs after starting, the contents of the folder `/opt/digiverso/goobi/activemq/` may be to blame. Emptying and restarting helps in this case:

```bash
find /opt/digiverso/goobi/activemq/ -type f -delete
```

#### **LayoutWizzard**

The `LayoutWizzard.jar` in `/opt/digiverso/{goobi,itm}/lib/` must be the same Symbolic links do not work.

## Implementation of the actual update

After all preliminary work has been carried out, the actual update can take place. This is explained in detail in individual steps here:

[Update steps](../02_update_steps/02_update_steps.md)