# Serverseitiges importieren

Sofern der serverseitige Austauschordner nicht leer ist, kann im Bereich für das serverseitige Importieren ein Ordner ausgewählt werden, aus denen die zu einem früheren Zeitpunkt exportierten Bilder nun in den aktuellen Vorgang importiert werden können.

![Serverseitiges Importieren von Dateien](30-55d.png)

Dazu muss definiert werden, an welche Stelle innerhalb der Paginierungssequenz die neue Datei eingefügt werden soll. Anschließend kann gewählt werden, ob die neuen Dateien als `uncounted` eingefügt werden sollen oder ob sie in die bestehende Paginierung integriert werden sollen.

Im Anschluss daran wird für jeden Ordner innerhalb des Austauschordners sein Pendant innerhalb des aktuellen Vorgangsordners gesucht. In diesen Ordner werden dann die gewählten Dateien importiert. Nach dem erfolgreichen Import der Dateien wird der Ordner im Austauschordner gelöscht.