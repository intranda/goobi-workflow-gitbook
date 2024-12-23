# goobi_opacUmlaut.txt

In der Konfigurationsdatei `goobi_opacUmlaut.txt` werden Umlaute angegeben, die beim automatischen Generieren von Vorgangstiteln ersetzt werden sollen. Die Datei befindet sich üblicherweise an folgendem Speicherpfad:

```bash
/opt/digiverso/goobi/config/goobi_opacUmlaut.txt
```

Beispielhaft sieht diese Konfigurationsdatei wie folgt aus:

{% code title="goobi_opacUmlaut.txt" %}
```apache
á a
ć c
é e
í i
ĺ l
ń n
ó o
ő o
ŕ r
ś s
ú u
ű u
ý y
ź z
ă a
ĕ e
ğ g
ĭ i
ŏ o
ŭ u
č c
ď d
ě e
ľ l
ň n
ř r
š s
ť t
ž z
ç c
ģ g
ķ k
ļ l
ņ n
ŗ r
ş s
ţ t
ä a
ë e
ï i
ö o
ü u
ÿ y
à a
è e
ì i
ò o
ù u
ā a
ē e
ī i
ō o
ū u
ą a
ę e
į j
ų u
ċ c
ḋ d
ė e
ḟ f
ġ g
ḣ h
i i
ı l
ṁ m
ṅ n
ṗ p
ṙ r
ṡ s
ṫ t
ż z
ḍ d
ḥ h
ḳ k
ḷ l
ṃ m
ṛ r
ṣ s
ṭ t
ṿ v
đ d
ŧ t
å a
ů u
ł l
ø o
ã a
ĩ i
ñ n
õ o
ũ u
â a
ĉ c
ê e
ĝ g
ĥ h
î i
ĵ j
ô o
ŝ s
û u
ŵ w
ŷ y
```
{% endcode %}

Üblicherweise werden die verwendeten Vorgangstitel von Goobi Workflow automatisch generiert. Diese beinhalten die Anfangsbuchstaben des Autors und eine Abkürzung des entsprechenden Werknamens.

Da der Vorgangstitel aus Kompatibilitätsgründen keine Umlaute bzw. Sonderzeichen beinhalten darf, versucht Goobi, diese durch kompatible Buchstaben mit ähnlicher Bedeutung zu ersetzen.

Während es für einen Anwender intuitiv ist, dass ein `ä` auch durch ein `a` ersetzt werden kann, haben diese beiden Buchstaben keinen technischen Zusammenhang. Daher muss dieser Zusammenhang im Sinne des Sprachgebrauchs konfiguriert werden. Üblicherweise ist die oben gezeigte Konfiguration bereits vorhanden und deckt die meisten Sprachen ab.

In der Datei `goobi_opacUmlaut.txt` werden die verwendeten Ersetzungsregeln angegeben. In der ersten Spalte stehen die zu ersetzenden Zeichen. Dahinter steht jeweils das Ersatzzeichen. Dieses darf selbst kein Sonderzeichen oder Umlaut sein.

Alle Sonderzeichen, die nicht in dieser Konfigurationsdatei berücksichtigt werden, werden beim Generieren des Vorgangstitels ersatzlos aus dem Namen entfernt.

Der Übersetzungsalgorithmus ist so implementiert, dass auch mehrbuchstabige Zeichenfolgen ersetzt werden können. Dabei ist auch folgende Konfiguration möglich, wobei immer genau ein Leerzeichen als Trennzeichen erwartet wird:

```apache
ä ae
ö oe
ü ue
Ä Ae
Ö Oe
Ü Ue
ß ss
```

Zu beachten ist, dass erst der Vorgangstitel anhand der Originalnamen generiert wird und danach die Umlaute ersetzt werden. Dabei kann es vorkommen, dass sich bei einer mehrbuchstabigen Ersetzung die Länge des Vorgangstitels ändert.

Ist zum Beispiel der Name des Autors `Björn` und es werden die ersten vier Buchstaben verwendet, ergibt sich das Kürzel `björ` (ohne Großschreibung). Da nun das `ö` zum `oe` wird, ändert sich die Abkürzung zu `bjoer` und hat nun fünf Buchstaben.