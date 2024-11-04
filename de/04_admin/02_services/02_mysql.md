# Datenbank MySQL

## **Allgemein**

Goobi nutzt zum Speichern von Informationen eine Datenbank. Hierfür wird grundsätzlich MySQL bevorzugt. Diese Datenbankengine wird vorzugsweise aus den Standardrepositories des Betriebssystems in der jeweils letzten stabilen Version installiert.

## **Beispiel: Ubuntu Linux 14.04 LTS**

MySQL wird unter Ubuntu Linux 14.04 LTS aus den Standard Repositories mit dem folgenden Befehl installiert:

```bash
sudo aptitude install mysql-server
```

Der Dienst kann mit diesen beiden Befehlen gestoppt und gestartet werden:

```bash
service mysql stop
service mysql start
```

Die Konfigurationsdateien für MySQL befinden sich im folgenden Pfad:

```bash
/etc/mysql/
```