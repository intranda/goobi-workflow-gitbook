# goobi_opacUmlaut.txt

In the configuration file `goobi_opacUmlaut.txt` umlauts are specified which should be replaced when automatically generating process titles. The file is usually located at the following location:

```bash
/opt/digiverso/goobi/config/goobi_opacUmlaut.txt
```

For example, this configuration file looks as follows:

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

Usually, Goobi Workflow automatically generates the process titles used. These contain the first letters of the author and an abbreviation of the corresponding work name.

Since the task title cannot contain umlauts or special characters for compatibility reasons, Goobi tries to replace them with compatible letters with similar meanings.

While it is intuitive for a user that an `ä` can also be replaced by an `a`, these two letters have no technical connection. Therefore, this context must be configured in terms of language usage. Usually the configuration shown above is already present and covers most languages.

In the file `goobi_opacUmlaut.txt` the used replacement rules are specified. The first column contains the characters to be replaced. Behind this is the replacement character. This may not be a special character or an umlaut.

All special characters, which are not considered in this configuration file, are removed without replacement from the name when generating the process title.

The translation algorithm is implemented in such a way that also multi-letter strings can be replaced. The following configuration is also possible, whereby exactly one space character is always expected as a separator:

```apache
ä ae
ö oe
ü ue
Ä Ae
Ö Oe
Ü Ue
ß ss
```

Please note that the process title is first generated using the original names and then the umlauts are replaced. Thereby it can happen that the length of the process title changes in case of a multi-letter substitution.

For example, if the author's name is `Björn` and the first four letters are used, the result is the abbreviation `björ` (without capitalization). Since the `ö` now becomes `oe`, the abbreviation changes to `bjoer` and now has five letters.