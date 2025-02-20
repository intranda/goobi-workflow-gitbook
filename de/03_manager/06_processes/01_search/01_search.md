# Vorgänge suchen

Möchten Sie gezielt nach Vorgängen suchen, stellt Goobi hierfür eine erweiterte Suchmaske zur Verfügung. Diese erreichen Sie über das Menü `Workflow` - `Vorgang suchen`.

![Erweiterte Maske für die Suche nach Vorgängen](screen1_de.png)

Für eine granulare Suche ist in diesem Zusammenhang relevant, dass auch diese Suchmaske Goobi-intern eine Filtersyntax verwendet, um damit die gesuchten Vorgänge aus der Datenbank zu ermitteln.

![Ergebnis der Suchanfrage nach Umwandlung der Anfrage in die interne Suchsyntax](screen2_de.png)

Aus den vorhergehenden Abbildungen wird deutlich, wie aus der Suchanfrage, die mittels der Suchmaske erfolgte, intern eine Suchabfrage auf der Basis der internen Suchsyntax durchgeführt wurde. Die generierte Suchanfrage ist im Filterfeld `Vorgänge filtern` oberhalb der Tabelle sichtbar und kann um zusätzliche Parameter erweitert werden. Außerdem ist es ebenfalls möglich, eine Suchanfrage dauerhaft zu speichern für den Fall, dass eine solche Suchanfrage häufiger aufgerufen werden soll.

Damit steht sie in der Auswahlliste der vordefinierten Filter zur Verfügung und kann jederzeit neu ausgeführt werden. Die hier im Hintergrund wirkende Filtersyntax soll in diesem Abschnitt beispielhaft erläutert werden. Dies ist aus dem Grunde sinnvoll, da mit einer manuellen Kombination der im Folgenden beschriebenen Suchparameter noch detailliertere Suchanfragen möglich sind, als diese durch die Suchmaske angeboten werden. In der folgenden Tabelle werden einige beispielhafte Filter zusammen mit deren Suchverhalten detailliert beschrieben.

## Die detaillierte Filtersyntax für Vorgänge an Beispielen

| Filtersyntax | Beschreibung der Filterfunktionalität |
| :--- | :--- |
| ab | Filtert nach allen Vorgängen aus allen Projekten, bei denen `ab` im Vorgangstitel vorkommt. |
| -ab | Filtert nach allen Vorgängen, bei denen `ab` im Vorgangstitel nicht vorkommt. |
| ab -abc | Filtert nach allen Vorgängen, bei denen `ab` im Vorgangstitel vorkommt, `abc` alerdings nicht. |
| a?c | Filtert nach allen Vorgängen, bei denen `a`, ein beliebiges Zeichen und `c` vorkommt. Nach dem Text `ac` wird mit `a?c` entsprechend nicht gesucht. |
| a\*c | Filtert nach allen Vorgängen, bei denen `a`, beliebig viele Zeichen und `c` vorkommt. Weil `\*` auch "keinem Zeichen" entsprechen kann, wird mit dem Text `a*c` auch nach `ac` gesucht. |
| meta:Shelfmark:123 | Filtert nach allen Vorgängen, die das Metadatum `Signatur (shelfmark)` mit dem Wert `123` enthalten. |
| meta:Author:Mustermann | Filtert nach allen Vorgängen, die das Metadatum `Author` mit dem Wert `Mustermann` enthalten. |
| "meta:Author:Max Mustermann" "meta:Author:John Doe" | Filtert nach allen Vorgängen, bei denen die beiden Autoren `Max Mustermann` und `John Doe` erfasst wurden. |
| meta:index.Person:Mustermann | Filtert nach allen Vorgängen, die im Personenindex den Wert `Mustermann` enthalten. |
| meta:\*:123 | Filtert nach allen Vorgängen, die in einem beliebigen Metadatum den Wert `123` enthalten. |
| -meta:Shelfmark:\* | Filtert nach allen Vorgängen, die keine `Signatur` haben. |
| batch:3 | Filtert nach allen Vorgängen, die dem `batch` mit der Nummer `3` zugeordnet sind. |
| -batch:3 | Filtert nach allen Vorgängen, die nicht dem `batch` mit der Nummer `3` zugeordnet sind. |
| journal:intranda | Filtert nach allen Vorgängen, die im `Journal` das Wort `intranda` enthalten. |
| project:sample_project | Filtert nach allen Vorgängen aus dem Projekt `sample_project`. |
| "project:sample project" | Filtert nach allen Vorgängen eines Projektes, wenn der Name des Projektes `Leerzeichen` beinhaltet. |
| ab project:sample_project | Filtert nach allen Projekten, die `ab` im Titel beinhalten und aus dem Projekt `sample_project` stammen. |
| ab -abc "project:sample project" | Filtert nach allen Vorgängen aus dem Projekt `sample project`, dessen Titel `ab` aber nicht `abc` enthält. |
| "-project:sample project" | Filtert nach allen Vorgängen, die nicht aus dem Projekt `sample project` stammen. |
| stepDone:7 | Filtert nach allen Vorgängen in allen Projekten, deren Workflowschritt mit der Reihenfolgennummer `7` bereits `abgeschlossen` wurde. |
| stepOpen:7 | Filtert nach allen Vorgängen, deren Arbeitsschritt mit der Reihenfolgennummer `7` auf eine Bearbeitung durch einen Benutzer `wartet`. |
| stepInFlight:7 | Filtert nach allen Vorgängen in allen Projekten, deren (automatischer) Arbeitsschritt mit der Reihenfolgennummer `7` derzeit `in einer Warteschlange` liegt. |
| stepInWork:7 | Filtert nach allen Vorgängen in allen Projekten, deren Arbeitsschritt mit der Reihenfolgennummer `7` innerhalb des Workflows sich derzeitig `in Bearbeitung` befindet. |
| stepLocked:7 | Filtert nach allen Vorgängen, deren Arbeitsschritt mit der Reihenfolgennummer `7` noch `gesperrt` ist. |
| stepDeactivated:7 | Filtert nach allen Vorgängen in allen Projekten, deren Arbeitsschritt mit der Reihenfolgennummer `7` derzeit `deaktiviert` ist. |
| stepError:7 | Filtert nach allen Vorgängen in allen Projekten, deren Arbeitsschritt mit der Reihenfolgennummer `7` in `einen Fehlerzustand geraten` ist. |
| stepDone:4 stepLocked:7 | Filtert nach allen Vorgängen, von denen mindestens der Arbeitsschritt `4` abgeschlossen, der Schritt `7` allerdings noch nicht `für die Bearbeitung frei gegeben` wurde. |
| stepInWork:Imaging | Filtert nach allen Vorgängen, deren Arbeitsschritt mit dem Titel `Imaging` sich gerade `in Bearbeitung` findet. |
| stepDone:Export "project:sample project" | Filtert nach allen Vorgängen, deren Arbeitsschritt mit dem Titel `Export` `bereits abgeschlossen` wurde und die zu dem Projekt mit dem Namen `sample project` gehören. |
| "id:17 18 19" | Filtert nach allen Vorgängen mit den internen Goobi-Identifiern `17`, `18` oder `19`. |
| template:123 | Filtert nach allen Vorgängen, deren `physische Vorlage` eine Eigenschaft enthält, deren Wert `123` beinhaltet. |
| template:shelfmark:123 intranda | Filtert nach allen Vorgängen, deren Eigenschaft `Signatur (shelfmark)` der physischen Vorlage den Wert `123` und der Titel des Vorgangs `intranda` enthält. |
| workpiece:intranda | Filtert nach allen Vorgängen, deren Eigenschaft des zugehörigen Werkstücks als Wert `intranda` enthält. |
| workpiece:Artist:intranda | Filtert nach allen Vorgängen, deren Werkstückeigenschaft `Artist` den Wert `intranda` enthält. |
| workpiece:Artist:intranda process:shelfmark:123 "project:sample project" stepDone:Imaging 456 | Filtert nach allen Vorgängen des Projektes sample project, die im Vorgangstitel `456` enthalten, von denen mindestens der Arbeitsschritt Imaging abgeschlossen ist, deren Signatur der physischen Vorlage `123` enthält und deren Werkstückeigenschaften als `Artist` `intranda`. |
| processproperty:Schrifttyp:fra | Filtert nach allen Vorgängen, deren Vorgangseigenschaft `Schrifttyp` den Wert `fra` enthält. |
| project:Berlin \|project:London | Oder-Suche nach allen Vorgängen, deren `Projekttitel` entweder `Berlin` oder `London` enthält. |
| "project:Palma de Mallorca" "\|project:New York" | Oder-Suche nach allen Vorgängen, deren `Projekttitel` entweder `Palma de Mallorce` oder `New York` enthält. Die einzelnen Suchparameter sind hier in `Anführungszeichen` gesetzt, da die Projekttitel hier Leerzeichen enthalten. |
| "meta:TitleDocMain:1801" "\|meta:TitleDocMain:1802" | Oder-Suche nach Vorgängen, deren Metadaten im `Haupttitel` `1801` oder `1802` enthält. Die `Anführungszeichen` sind hierbei nur dann nötig, wenn innerhalb des Suchbegriffs Leerzeichen enthalten sind. |
| processdate=2021 | Sucht nach Vorgängen, deren `Erstellungszeitpunkt` im Jahr `2021` liegt. |
| processdate!=2021 | Sucht nach Vorgängen, deren `Erstellungszeitpunkt` nicht im Jahr `2021` liegt. |
| "processdate&lt;2020-01-01 12:00:00" | Sucht nach Vorgängen, deren `Erstellungszeitpunkt` vor dem `01.01.2020 12:00:00` liegt. |
| processdate&gt;2020-01-01 processdate&lt;2020-12-31 | Sucht nach Vorgängen, deren `Erstellungszeitpunkt` nach dem `01.01.2020` und vor dem `31.12.2020` liegt. |
| stepdone:Scanning stepfinishdate:2021 | Sucht nach Arbeitsschritte mit dem Titel `Scanning`, die im Jahr `2021` abgeschlossen wurden. |
| stepstartdate:2021 | Sucht nach Arbeitsschritten, deren Bearbeitung im Jahr `2021` begonnen hat. |
| stepdone:Scanning "stepdone:Quality control" stepfinishdate:2021 | Sucht nach den Arbeitsschritten `Scanning` und `Quality control`, die beide im Jahr `2021` abgeschlossen wurden. |
| stepdone:Scanning stepfinishdate&gt;2021-08-01 stepfinishdate&lt;2021-08-31 | Sucht nach Arbeitsschritten `Scanning`, die im `August 2021` abgeschlossen wurden. |
| stepDone:Scanning processdate=2021 \|processdate=2022 | Sucht nach Vorgängen, die im Jahr 2022 erstellt wurden oder einen Arbeitsschritt `Scanning` haben und im Jahr 2021 erstellt wurden. |
| stepDone:Scanning (processdate=2021 \|processdate=2022) | Sucht nach Vorgängen, die einen Arbeitsschritt `Scanning` haben und entweder im Jahr 2021 oder im Jahr 2022 erstellt wurden. Klammern können beliebig geschachtelt werden, um die Priorität und damit die Ausführreihenfolge der einzelnen UND- und ODER-Bedingungen zu bestimmten. |

**Hinweis:** Die Operatoren `<` und `>` werden im Hintergrund als `kleiner gleich` und `größer gleich` interpretiert. Wird zum Beispiel nach `processdate>2022` gesucht, so werden alle Vorgänge aufgelistet, deren Erstelldatum 2022 und später ist.

Wie Sie an den Beispielen der Filter erkennen können, sind über die freie Kombinierbarkeit verschiedenster Parameter miteinander auch sehr komplexe Filteranfragen möglich. Im Gegensatz zur einfach zu bedienenden Filtermaske können mittels der Suchsyntax auch gleiche Parameter mit unterschiedlichen Werten mehrfach innerhalb einer Anfrage verwendet werden (z.B. die gleichzeitige Suche nach abgeschlossenen sowie nach offenen Arbeitsschritten eines Workflows).

Sämtliche der hier aufgeführten Parameter sind beliebig untereinander kombinierbar. Bitte beachten Sie, dass jeder Parameter, der Leerzeichen beinhaltet, stets von Anführungszeichen eingeschlossen wird.