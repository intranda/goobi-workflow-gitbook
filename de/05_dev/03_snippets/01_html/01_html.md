# HTML

## Formular-Komponenten

### Textfeld (einzeilig)

Das Attribut `for="..."` für das Label ist optional.

```xml
<!-- INPUT TEXT -->
<div class="form-group">
    <label for="exampleInputText">Textfeld</label>
    <input type="text" id="exampleInputText" class="form-control" placeholder="Placeholder Text" />
</div>
```

### Textfeld (mehrzeilig)

Das Attribut `for="..."` für das Label ist optional.

```xml
<!-- INPUT TEXTAREA -->
<div class="form-group">
    <label for="exampleInputTextarea">Textarea</label>
    <textarea id="exampleInputTextarea" class="form-control"></textarea>
</div>
```

### Auswahlmenü (einfache Auswahl)

Das Attribut `for="..."` für das Label ist optional.

```xml
<!-- SELECT MENU -->
<div class="form-group">
    <label for="exampleFormControlSelect1">Select Menü</label>
    <div class="form-control form-control--select">
        <select id="exampleFormControlSelect1">
            <option>1</option>
            <option>2</option>
            <option>3</option>
            <option>4</option>
            <option>5</option>
        </select>
    </div>
</div>
```

### Auswahlmenü (mehrfache Auswahl)

Das Attribut `for="..."` für das Label ist optional.

```xml
<!-- MULTISELECT MENU -->
<div class="form-group">
    <label for="exampleFormControlSelect2">Multiselect Menü</label>
    <select multiple class="form-control" id="exampleFormControlSelect2">
        <option>1</option>
        <option>2</option>
        <option>3</option>
        <option>4</option>
        <option>5</option>
    </select>
</div>
```

### Datei hochladen

Das Attribut `for="..."` für das Label muss **nicht** gesetzt werden. Den Attributen `data-before` und `data-after` können mittels einer Message-Key-Methode `#{msgs.[einMessageKey]}` die Texte für die Eingabefelder übergegeben werden.

```xml
<!-- FILE -->
<label class="form-control form-control--file">
    <input type="file" id="inputTypeFileId" name="inputTypeFile">
    <span class="form-control--file-custom" data-before="[Text für before]" data-after="[Text für after]"></span>
</label>
```

### Checkboxen

Als Standard werden die Checkboxen in einer horizontalen Reihe aufgelistet. Das Attribut `for="..."` für das Label **muss** gesetzt werden, damit die korrekte Checkbox ausgewählt wird.

```xml
<!-- INPUT CHECKBOX -->
<div class="form-check">                                
    <label for="defaultCheck1">
        <input class="form-check-input" type="checkbox" value="" id="defaultCheck1">
        <span>
            <i class="fa fa-square-o" aria-hidden="true"></i>
            <i class="fa fa-check-square-o" aria-hidden="true"></i>
        </span>
        Default checkbox
    </label>
    <label for="defaultCheck2">
        <input class="form-check-input" type="checkbox" value="" id="defaultCheck2">
        <span>
            <i class="fa fa-square-o" aria-hidden="true"></i>
            <i class="fa fa-check-square-o" aria-hidden="true"></i>
        </span>
        Default checkbox
    </label>
</div>
```

Möchte man sie untereinander angeordnet haben, so ergänzt man die CSS-Klasse `form-check` um die CSS-Klasse `form-check--block.`

```xml
<!-- INPUT CHECKBOX BLOCK -->
<div class="form-check form-check--block">...</div>
```

### Radio-Buttons

Als Standard werden die Radio-Buttons in einer horizontalen Reihe aufgelistet. Das Attribut `for="..."` für das Label **muss** gesetzt werden, damit der korrekte Radio-Button ausgewählt wird.

```xml
<!-- INPUT CHECKBOX -->
<div class="form-check">                                
    <label for="defaultRadio1">
        <input class="form-check-input" type="radio" value="" id="defaultRadio1">
        <span>
            <i class="fa fa-circle-o" aria-hidden="true"></i>
            <i class="fa fa-check-circle-o" aria-hidden="true"></i>
        </span>
        Default checkbox
    </label>
    <label for="defaultRadio2">
        <input class="form-check-input" type="radio" value="" id="defaultRadio2">
        <span>
            <i class="fa fa-circle-o" aria-hidden="true"></i>
            <i class="fa fa-check-circle-o" aria-hidden="true"></i>
        </span>
        Default checkbox
    </label>
</div>
```

Möchte man sie untereinander angeordnet haben, so ergänzt man die CSS-Klasse `form-check` um die CSS-Klasse `form-check--block.`

```xml
<!-- INPUT CHECKBOX BLOCK -->
<div class="form-check form-check--block">...</div>
```

## Formular-Gruppen

Die oben aufgeführte Formular-Komponenten sind in den Formular-Gruppen verwendbar. Die Spalten (col) sind nach den [Bootstrap 4 Grid](https://getbootstrap.com/docs/4.3/layout/grid/) Regeln zu verwenden. Die folgenden Beispiele sind auf zwei- und dreispaltige Formular-Gruppen ausgelegt.

### Formular-Gruppe (dreispaltig)

Das Attribut `for="..."` für das Label ist optional. Das Label kann auch durch einen `<span>...</span>` ersetzt werden.

```xml
<div class="form-group form-group--flex">
    <div class="row justify-content-between">
        <div class="col-3">
            <label for="exampleInputText">Form Group Flex</label>
        </div>
        <div class="col-7">
            <input type="text" id="exampleInputText" class="form-control" placeholder="Placeholder Text" />
        </div>
        <div class="col-2">
            <button type="button" class="btn btn--icon-light">
                <i class="fa fa-search" aria-hidden="true"></i>
            </button>
        </div>
    </div>
</div>
```

### Formular-Gruppe (zweispaltig)

Das Attribut `for="..."` für das Label ist optional. Das Label kann auch durch einen `<span>...</span>` ersetzt werden.

```xml
<div class="form-group form-group--flex">
    <div class="row justify-content-between">
        <div class="col-3">
            <label for="exampleInputText">Form Group Flex</label>
        </div>
        <div class="col-9">
            <input type="text" id="exampleInputText" class="form-control" placeholder="Placeholder Text" />
        </div>
    </div>
</div>
```

## Boxen

Boxen sind standardmäßig blau und nicht ein- und ausklappbar. Die Farbe und Funktionalität kann durch ergänzende CSS-Klassen verändert werden. Der Bereich `module__box-title-actions` ist optional.

### Standard Box

```xml
<!-- MODULE BOX -->
<div class="module module__box">
    <!-- BOX TITLE -->
    <div class="module__box-title">
        <h3>
            <i class="fa fa-bars" aria-hidden="true"></i>
            <span>STANDARD BOX</span>
            <button type="button" class="btn btn--clean" data-toggle="box-body">
                <i class="fa fa-angle-up fa-lg" aria-hidden="true"></i>
            </button>
        </h3>
        <!-- BOX TITLE ACTIONS -->
        <div class="module__box-title-actions">
            <button type="button" class="btn btn--icon">
                <i class="fa fa-refresh" aria-hidden="true"></i>
            </button>
        </div>
    </div>
    <!-- BOX BODY -->
    <div class="module__box-body">
        CONTENT GOES HERE...
    </div>
</div>
```

### Standard Box (ein- und ausklappbar)

```xml
<!-- MODULE BOX COLLAPSABLE -->
<div class="module module__box module__box--collapsable">
    SAME AS MODULE BOX...
</div>
```

### Box (grau)

```xml
<!-- MODULE BOX GRAY -->
<div class="module module__box module__box--gray">
    SAME AS MODULE BOX...
</div>
```

### Box (weiß)

```xml
<!-- MODULE BOX WHITE -->
<div class="module module__box module__box--white">
    SAME AS MODULE BOX...
</div>
```

### Box (komplett)

Gilt für alle Farbmöglichkeiten.

```xml
<!-- MODULE BOX COMPLETE -->
<div class="module module__box module__box--collapsable module__box--white">
    SAME AS MODULE BOX...
</div>
```

## Buttons

Es gibt mehrere Arten von Buttons, die alle die CSS-Klasse `btn` als Elternklasse haben. Die Modifikationen der Buttons werden durch zusätzliche CSS-Klassen gesteuert. Die Icons in den Buttons können beliebig durch ein Icon der Bibliothek von [Font Awesome 4](https://fontawesome.com/v4.7.0/icons/) ausgetauscht werden.

```xml
<!-- BUTTON DEFAULT -->
<button type="button" class="btn btn--default">Button default</button>
<!-- BUTTON SUCCESS -->
<button type="button" class="btn btn--success">Button success</button>
<!-- BUTTON DANGER -->
<button type="button" class="btn btn--danger">Button danger</button>
<!-- BUTTON FULL -->
<button type="button" class="btn btn--full">Button full</button>
<!-- BUTTON CLEAN -->
<button type="button" class="btn btn--clean">Button clean</button>
<!-- BUTTON INACTIVE -->
<button type="button" class="btn btn--inactive">Button inactive</button>
<!-- BUTTON GRAY -->
<button type="button" class="btn btn--gray">Button gray</button>
<!-- BUTTON LINK -->
<button type="button" class="btn btn--link">Button link</button>
<!-- BUTTON HIDDEN -->
<button type="button" class="btn btn--hidden">Button hidden</button>
<!-- BUTTON VISUALY HIDDEN -->
<button type="button" class="btn btn--vhidden">Button visualy hidden</button>
<!-- BUTTON ICON -->
<button type="button" class="btn btn--icon">
    <i class="fa fa-refresh" aria-hidden="true"></i>
</button>
<!-- BUTTON ICON GRAY -->
<button type="button" class="btn btn--icon-gray">
    <i class="fa fa-refresh" aria-hidden="true"></i>
</button>
<!-- BUTTON ICON LIGHT -->
<button type="button" class="btn btn--icon-light">
    <i class="fa fa-refresh" aria-hidden="true"></i>
</button>
<!-- BUTTON ICON WHITE -->
<button type="button" class="btn btn--icon-white">
    <i class="fa fa-refresh" aria-hidden="true"></i>
</button>
<!-- BUTTON ICON BLUE -->
<button type="button" class="btn btn--icon-blue">
    <i class="fa fa-refresh" aria-hidden="true"></i>
</button>
```

### Button Toggle

Eine Besonderheit für einen Button gibt es noch. Wird die CSS-Klasse `btn--toggle` an einen Button vergeben und als nächstes Element ein `<div />` gesetzt, so kann dieses DIV auf- und zugeklappt werden.

```xml
<!-- BUTTON TOGGLE -->
<button type="button" class="btn btn--icon btn--toggle">
    <i class="fa fa-exchange" aria-hidden="true"></i>
    Button toggle
</button>
<div>
    CONTENT GOES HERE...
</div>
```

### Button mit AJAX Loader

Ein weiterer Spezial-Button wird durch die CSS-Klasse `btn--loader` aktiviert. Wird diese Klasse vergeben, so wird während eines AJAX-Request `<f:ajax />` ein animierter Loader im geklickten Button angezeigt und nach Abschluss des Requests wieder ausgeblendet.

```xml
<h:commandLink
    id="myActionButton"  
    styleClass="btn btn--gray btn--loader" 
    action="#{myBean.myMethod}" 
    title="myButtonTitle">
    <i class="fa fa-search" aria-hidden="true"></i>
    <span class="btn-ajax-loader" aria-hidden="true">
        <img src="template/img/goobi/ajaxloader2.gif" alt="Ajax Button Loader" />
    </span>
    <f:ajax execute="@form" render="myRenderArea" />
</h:commandLink>
```