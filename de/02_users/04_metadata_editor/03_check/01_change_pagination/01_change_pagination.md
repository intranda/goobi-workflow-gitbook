# Paginierung nachträglich ändern

Einmal erstellte Paginierungssequenzen können zu einem späteren Zeitpunkt erneut verändert werden. Dabei können einzelne Seiten oder mehrere Seiten auf einmal verschoben oder gelöscht werden. Dazu müssen zunächst die gewünschten Seiten in der Box `Seitenauswahl` ausgewählt werden. Wenn mindestens eine Seite auf diese Weise markiert wurde, stehen die folgenden Funktionen zur Verfügung:

| Icon                                                             | Beschreibung                              |
| ---------------------------------------------------------------- | ----------------------------------------- |
| ![screen1.png](<screen1.png>)    | Ausgewählte Seiten nach oben verschieben  |
| ![screen2.png](<screen2.png>)    | Ausgewählte Seiten nach unten verschieben |
| ![screen3.png](<screen3.png>) | Ausgewählte Seiten löschen                |

Unabhängig von der Auswahl einer Seite steht darüber hinaus ebenso die folgende Funktion zur Verfügung:

| Icon                                                         | Beschreibung            |
| ------------------------------------------------------------ | ----------------------- |
| ![screen4.png](<screen4.png>) | Dateinamen neu erzeugen |

Wenn eine oder mehrere Seiten nach oben verschoben werden, tauscht jede Seite mit dem Vorgänger in der Paginierung ihren Platz. Dabei werden alle Einstellungen und Seitenzuweisungen des Vorgängers übernommen. Wenn Seiten nach unten verschoben werden, tauschen sie auf die gleiche Art ihren Platz mit dem Nachfolger in der Paginierung.

Ist von diesen Änderungen das aktuell angezeigte Bild betroffen, wird die Bildnummer in der Seitenanzeige automatisch aktualisiert. Das angezeigte Bild bleibt bestehen.

Neben dem Verschieben von Dateien ist es auch möglich, ausgewählte Dateien zu löschen. Dabei wird die ausgewählte Seite aus der Metadatendatei komplett entfernt. Dies betrifft sowohl die Dateinamen-Zuweisung als auch die Zuordnung zu Strukturelementen oder zugeordnete Metadaten.

Zusätzlich wird die Datei aus allen Ordnern des Vorgangs gelöscht. Die Suche der zu löschenden Dateien aus allen Vorgangs-Ordnern erfolgt auf Basis des Dateinamen, der ausgewählt wurde. Dabei werden in den vorhandenen Ordnern nach den Dateien gesucht, die dem Dateinamen mit Ausnahme einer eventuell abweichenden Dateiendung entsprechen.

Das Löschen erfolgt in allen Unterordnern der Verzeichnisse `ocr` und `images`. Sollte das aktuell angezeigte Bild gelöscht worden sein, wird stattdessen das erste Bild angezeigt. Ansonsten wird die Bildnummer aktualisiert.

Damit auch Systeme, die nicht auf der Sequenz der Dateinamen in der METS-Datei basieren, weiterhin in der Lage sind, die Objekte in der richtigen Reihenfolge zu zeigen, gibt es die Funktion, die Dateinamen neu zu erzeugen. Dabei werden auf Basis der Reihenfolge in der METS-Datei alle Dateien acht-stellig durchnummeriert. Diese Umbenennung erfolgt ebenfalls in allen Ordnern des Vorgangs.