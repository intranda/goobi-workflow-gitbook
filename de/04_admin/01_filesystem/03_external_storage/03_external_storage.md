# Einbindung von externem Storage

## **Allgemeines**

Da in Digitalisierungsprojekten im Allgemeinen mit sehr großen Datenmengen gearbeitet wird, muss zumeist externer Speicher an den Server angebunden werden. Dieses ist technisch unterschiedlich lösbar. Empfohlen wird, den externen Speicher grundsätzlich in den folgenden Ordner im Verzeichnisbaum einzuhängen:

```bash
/opt/digiverso/
```

Somit finden sich sämtliche Daten von Goobi an einem zentralen Ort.

Im Folgenden werden zwei Möglichkeiten für die Einbindung von externem Speicher schemenhaft aufgezeigt. Von einer Anbindung über CIFS sollte aufgrund schlechter Performance und fehlender Funktionalität grundsätzlich abgesehen werden. Auch sind über CIFS keine symbolischen Links oder Nur-Lese-Rechte abbildbar.

## **NFS Share**

Um einen externen Speicher über einen NFS Share einzubinden, werden die folgenden Informationen benötigt:

• exportierender Server  
• exportiertes Verzeichnis

Anschließend kann der Speicher per NFS in den Verzeichnisbaum eingehängt werden. Hierfür bietet es sich an, einen Eintrag in die Datei /etc/fstab hinzuzufügen, die die Verbindung beim Systemstart automatisch herstellt. Ein beispielhafter Eintrag sieht wie folgt aus:

```bash
example.net:/path/to/share /opt/digiverso nfs vers=3,rsize=8192,wsize=8192,soft,intr,rw,auto 0 0
```

## **Logisches Volume in der virtuellen Maschine**

Eine weitere Alternative, um externen Speicher einzubinden, ist diesen als eigenständiges Device an die virtuelle Maschine anzuhängen. 

Dieses können z.B. verschiedene iSCSI oder SAN LUNs sein. Sie werden später in der virtuellen Maschine zu einem Logischen Volume mittels LVM zusammengefasst. Das Ergebnis ist ein Speicher, der aus den verschiedenen Devices aggregiert wurde.