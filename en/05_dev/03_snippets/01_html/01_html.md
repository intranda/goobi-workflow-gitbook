# HTML

## Form components

### Text field (single-line)

The attribute `for="..."` for the label is optional.

```xml
<!-- INPUT TEXT -->
<div class="form-group">
    <label for="exampleInputText">Textfeld</label>
    <input type="text" id="exampleInputText" class="form-control" placeholder="Placeholder Text" />
</div>
```

### Text field (multiline)

The attribute `for="..."` for the label is optional.

```xml
<!-- INPUT TEXTAREA -->
<div class="form-group">
    <label for="exampleInputTextarea">Textarea</label>
    <textarea id="exampleInputTextarea" class="form-control"></textarea>
</div>
```

### Selection menu (simple selection)

The attribute `for="..."` for the label is optional.

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

### Selection menu (multiple selection)

The attribute `for="..."` for the label is optional.

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

### Upload file

The attribute `for="..."` for the label does **not** have to be set. The attributes `data-before` and `data-after` can be given the texts for the input fields by means of a message key method `#{msgs.[einMessageKey]}`.

```xml
<!-- FILE -->
<label class="form-control form-control--file">
    <input type="file" id="inputTypeFileId" name="inputTypeFile">
    <span class="form-control--file-custom" data-before="[Text für before]" data-after="[Text für after]"></span>
</label>
```

### Checkboxes

By default, the checkboxes are listed in a horizontal row. The attribute `for="..."` for the label **must** be set so that the correct checkbox is selected.

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

If you want them to be arranged one below the other, add the CSS class `form-check` to the CSS class `form-check--block.`

```xml
<!-- INPUT CHECKBOX BLOCK -->
<div class="form-check form-check--block">...</div>
```

### Radio-Buttons

By default, the radio buttons are listed in a horizontal row. The attribute `for="..."` for the label **must** be set so that the correct radio button is selected.

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

If you want them to be arranged one below the other, add the CSS class `form-check` to the CSS class `form-check--block.`

```xml
<!-- INPUT CHECKBOX BLOCK -->
<div class="form-check form-check--block">...</div>
```

## Form groups

The form components listed above can be used in the form groups. The columns (col) are to be used according to the [Bootstrap 4 Grid](https://getbootstrap.com/docs/4.3/layout/grid/) rules. The following examples are designed for two- and three-column form groups.

### Form group (three-column)

The attribute `for="..."` for the label is optional. The label can also be replaced by a `<span>...</span>`.

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

### Form group (two-column)

The attribute `for="..."` for the label is optional. The label can also be replaced by a `<span>...</span>`.

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

## Boxes

Boxes are blue by default and are not collapsible or expandable. The colour and functionality can be changed by supplementary CSS classes. The area `module__box-title-actions` is optional.

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

### Standard Box (extendable and collapsible)

```xml
<!-- MODULE BOX COLLAPSABLE -->
<div class="module module__box module__box--collapsable">
    SAME AS MODULE BOX...
</div>
```

### Box (grey)

```xml
<!-- MODULE BOX GREY -->
<div class="module module__box module__box--gray">
    SAME AS MODULE BOX...
</div>
```

### Box (white)

```xml
<!-- MODULE BOX WHITE -->
<div class="module module__box module__box--white">
    SAME AS MODULE BOX...
</div>
```

### Box (complete)

Applies to all colour options.

```xml
<!-- MODULE BOX COMPLETE -->
<div class="module module__box module__box--collapsable module__box--white">
    SAME AS MODULE BOX...
</div>
```

## Buttons

There are several types of buttons, all of which have the CSS class `btn` as their parent class. The modifications of the buttons are controlled by additional CSS classes. The icons in the buttons can be arbitrarily replaced by an icon from the library of [Font Awesome 4](https://fontawesome.com/v4.7.0/icons/).

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

There is one more special feature for a button. If the CSS class `btn--toggle` is assigned to a button and a `<div />` is set as the next element, this DIV can be expanded and collapsed.

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

### Button with AJAX Loader

Another special button is activated by the CSS class `btn--loader`. If this class is assigned, an animated loader is displayed in the clicked button during an AJAX request `<f:ajax />` and hidden again after the request is completed.

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