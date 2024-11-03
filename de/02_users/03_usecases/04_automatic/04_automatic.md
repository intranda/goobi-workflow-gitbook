# Automatische Skriptschritte

Neben den im vorherigen Abschnitt beschriebenen manuellen Skriptschritten kann Goobi auch so konfiguriert werden, dass einzelne Arbeitsschritte, die für den Aufruf von Skripten konfiguriert wurden, vollautomatisch ausgeführt werden.

Dazu vergibt der Administrator ähnlich wie für die manuellen Skriptschritte eine Reihe verschiedener `Shell-Kommandos` und definiert, dass diese in der vorgegebenen Reihenfolge vollautomatisch nacheinander durchlaufen werden sollen. Automatische Skriptschritte werden normalerweise nicht in der Aufgabenliste eines Nutzers aufgelistet. 

Findet im Rahmen der Ausführung der konfigurierten serverseitigen Skriptaufrufe ein Fehler statt und das Skript kann nicht erfolgreich ausgeführt werden, bleibt der automatische Arbeitsschritt in diesem Status stehen und wird somit automatisch bei dem zugewiesenen Benutzer angezeigt. Automatische Skriptschritte werden folglich nur dann für einen Nutzer in seiner Aufgabenliste sichtbar, wenn Fehler bei der Ausführung aufgetreten sind. 

Zur Ermittlung des aufgetretenen Fehlers erhält der Nutzer in gleicher Weise wie bei dem zuvor angesprochenen manuellen Skriptschritten die Möglichkeit, diese Skripte nun durch gezieltes Klicken manuell zu starten und die Ursache des Fehlers zu ermitteln. Sofern die automatischen Skripte von der Funktionalität Gebrauch machen, Informations- oder Fehlermeldungen zum Goobi-Vorgang zu senden, sind die Fehlermeldungen im `Vorgangslog` innerhalb des Arbeitsschritts ebenfalls aufgeführt, ohne dass der Skriptaufruf zur Ermittlung des aufgetretenen Fehlers erneut stattfinden muss.

Automatische Skriptschritte, die ohne Fehler die konfigurierten Skripte ausführen konnten, schließen automatisch den aktuellen Arbeitsschritt ab und aktivieren den nachfolgenden Arbeitsschritt innerhalb des Workflows.