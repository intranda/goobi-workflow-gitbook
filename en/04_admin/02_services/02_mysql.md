# MySQL database

## **General**

Goobi saves information using a database. As a rule, the preferred option is MySQL. Ideally, the latest stable version of this database engine is installed from the operating system’s standard repositories.

## **Example: Ubuntu Linux 14.04 LTS**

If you are using Ubuntu Linux 14.04 LTS, MySQL is installed from the standard repositories by means of the following command:

```bash
sudo aptitude install mysql-server
```

The service can be stopped and started using the following commands:

```bash
service mysql stop
service mysql start
```

The configuration data for MySQL is located on the following path:

```bash
/etc/mysql/
```