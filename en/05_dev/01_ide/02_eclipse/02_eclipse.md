# Setting up Eclipse

## 1.2.1 Starting Eclipse
After downloading the required components, Eclipse can be started. Depending on the operating system, this is usually possible by double-clicking. When asked for the location of the workspace, the following path can be entered here, for example:

```bash
/opt/digiverso/dev/workspace/
```

![Workspace](screen_workspace.png)

The installation directory now looks like this:

![Installation directory](screen_folder.png)


## 1.2.2 Configuring Eclipse

### SSH Key
Within Eclipse, you should configure your own SSH key to authenticate with the Git repositories. This is done within the Eclipse settings in the dialogue area `General` - `Network Connections` - `SSH2`. A private SSH key can be added there:

![SSH-Key](screen_ssh_key.png)


### Git properties
In addition, the following two properties `email` and `user` should be correctly configured for the use of Git. This can be done within the Eclipse settings in the section `Version Control (Team)` - `Git` - `Configuration`. There the two parameters `user.name` and `user.email` should be set.

![Git properties](screen_git.png)


### Setting up the Tomcat Server
Within the properties of Eclipse, the already unpacked Apache Tomcat can be set up under `Server` - `Runtime Environments`. The installed Tomcat is selected there.

![Setting up Tomcat Server](screen_tomcat1.png)

It should be noted that the correct JRE is also selected:

![Note Java version](screen_jre.png)


## 1.2.3 Installing Lombok for Eclipse
Within Goobi workflow we use the program library `Lombok`. This must be installed in addition to Eclipse. There are two possible ways to do this:

### Installation from Eclipse
The easiest way is to install from within Eclipse. First open the following dialogue via the menu `Help` - `Install New Software`:

![Installation from Eclipse](screen_lombok1.png)

Here, the installation URL from which the plugin is to be obtained must now be entered in the `Work with` input field. The following URL is used for this:

```text
https://projectlombok.org/p2
```

Afterwards, only the plugin `Lombok` must be selected in the lower area of the dialogue window. On the following pages of the dialogue, there is another security query regarding the certificate, which must be confirmed. After restarting Eclipse, the installation is complete.


### Manual installation
For manual installation, Lobok must first be downloaded from this URL: https://projectlombok.org/download

After the download, Lombok can be started by double-clicking. If it is not possible to start via a double-click, it is also possible to start via the command line:

```bash
cd ~/Downloads
java -jar lombok.jar
```

After starting, the already installed Eclipse can now be added there in order to then have Lobok added to the Eclipse installation.

![Manual Installation](screen_lombok2.png)


## 1.2.4 Checking out Goobi workflow from Git repository
After setting up Eclipse, Goobi can now be checked out as a project. To do this, simply open the following dialogue via the menu item `File` and then `Import`:

![Import dialogue](screen_import1.png)

In the following dialogue pages, Git is specified as the source for the import.

![Import dialogue](screen_import2.png)

There the item `Clone URI` is selected.

![Import dialogue](screen_import3.png)

Then the URL of the Goobi workflow Git repository can be specified. For GitHub the URL is:

```text
git@github.com:intranda/goobi-workflow.git
```

For the use of the intranda Gitea system, the URL is:

```text
git@gitea.intranda.com:goobi-workflow/goobi-workflow.git
```

In both cases, the URL should be chosen in such a way that authentication can take place via an SSH key that has been set up beforehand. Of course, the respective Git systems (GitHub or Gitea) must have the appropriate public SSH key. In the intermediate dialogue, the use of the SSH key must be confirmed again during the first check-out. You will then be taken to the other dialogue windows.

![Import dialogue](screen_import4.png)

In the penultimate dialogue window, you can now select that the project is an existing Eclipse project.

After the last dialogue window, the project is checked out and visible in the Eclipse workspace. First of all, the project is compiled by Eclipse and any dependencies are loaded.

![Eclipse with Goobi workflow checked out](screen_import5.png)

If dependencies are still missing, as shown in the previous screenshot, this can be remedied by right-clicking on the project and selecting the menu items `Maven` - `Update Project`.

![Update Maven dependencies](screen_import6.png)


## 1.2.5 Starting Goobi workflow for the first time
To start Goobi workflow from Eclipse for the first time, you can click on the items 'Run As' and 'Run on Server' in the context menu of the project.

![Launch Goobi](screen_start1.png)

Then the correct server must be selected. Here we take the previously installed Apache Tomcat and name it `goobi`.

![Select server](screen_start2.png)

On the following page, the display is simply confirmed.

![Confirm](screen_start3.png)

Goobi workflow now starts automatically and opens a browser window. However, the database connection is not yet correct. Therefore, some error messages still appear in the console in Eclipse.

![First start shows error](screen_start4.png)

Switching to the `Servers View` in the lower area allows us to stop the server again (red icon).

![Servers View](screen_start5.png)

In order to configure the database connection correctly, the project `Servers` is now opened in the left area and the file `servers.xml` is entered. There you can see the automatically added element `Context` within `Host` in the lower area:

![File servers.xml](screen_context1.png)

We now replace this element with the following content:

```xml
<Context docBase="Goobi" path="/goobi" reloadable="true" source="org.eclipse.jst.jee.server:Goobi">

    	<Resources allowLinking="true">
    	    <PostResources className="org.apache.catalina.webresources.DirResourceSet"
            base="/opt/digiverso/goobi/plugins/GUI/"
            webAppMount="/WEB-INF/lib"/>
    	    <!--
			<PostResources className="org.apache.catalina.webresources.DirResourceSet"
            base="/opt/digiverso/goobi/lib"
            webAppMount="/WEB-INF/lib"/>
			-->
    	</Resources>

    	<Resource name="goobi"
    	    auth="Container"
    	    driverClassName="software.aws.rds.jdbc.mysql.Driver"
    	    username="goobi"
    	    password="goobi"
    	    removeAbandoned="true"
    	    logAbandoned="true"
    	    maxActive="100"
    	    maxIdle="30"
    	    maxWait="10000"
    	    type="javax.sql.DataSource"
    	    minIdle="4"
    	    testOnBorrow="true"
    	    testWhileIdle="true"
    	    validationQuery="SELECT SQL_NO_CACHE 1"
    	    removeAbandonedTimeout="600"
    	    url="jdbc:mysql://localhost/goobi?characterEncoding=UTF-8&amp;autoReconnect=true&amp;autoReconnectForPools=true" />
</Context>
```

Note that the closing tag of `Host` was usually on the same line as the previous element `Context` (see previous screenshot). This must not be accidentally overwritten. Afterwards, the file should look like this.

![Extended file servers.xml](screen_context2.png)


## 1.2.6 Complete launch of Goobi workflow
All components of Goobi workflow are now set up correctly. Within the `Servers View` the Tomcat server can now be restarted (green icon). No error is visible in the console anymore. The web browser can now be accessed with this URL:

```text
http://localhost:8080/goobi/
```

A login is now possible on the start page of Goobi workflow with the login `goobi` and the password `goobi`.

![Goobi workflow ready for use](screen_login.png)