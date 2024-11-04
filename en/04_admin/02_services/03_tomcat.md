# Apache Tomcat servlet container

## General

Goobi is a web-based Java application. The Java code needs to be translated to ensure that Goobi can be called from your web browser. This job is done by a servlet container. Some examples are given below:

| Servlet Container | Project-URL |
| :--- | :--- |
| Apache Tomcat | [http://tomcat.apache.org/](http://tomcat.apache.org/) |
| Jetty | [http://jetty.codehaus.org/jetty/](http://jetty.codehaus.org/jetty/) |
| Resin | [http://onjava.com/pub/a/onjava/2002/09/18/resin.htm](http://onjava.com/pub/a/onjava/2002/09/18/resin.html) |

Goobi is usually installed in an `Apache Tomcat`. This servlet container is installed from the operating system’s standard repositories. However, if the standard repositories do not contain version 7, `Apache Tomcat` is installed and maintained manually.

## Example: Ubuntu Linux 14.04 LTS

If you are using Ubuntu Linux 14.04 LTS, you need to use the following command to install Apache Tomcat \(version 7\) from the standard repositories:

```bash
sudo aptitude install tomcat7
```

The service can be stopped and started using the following commands:

```bash
service tomcat7 stop
service tomcat7 start
```

The configuration data is located in the following path:

```bash
/etc/tomcat7/
/etc/default/tomcat7/
```

In order to install Goobi, you have to place the file goobi.war into the Tomcat’s webapps folder. The file is unpacked automatically. The webapps folder is located on the following path:

```bash
/var/lib/tomcat7/webapps/
```