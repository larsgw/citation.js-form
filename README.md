# Citation.js Form

##### Table of Contents

* [Use](#use)
  * [jQueryCite](#cite)
    * [HTML templates](#cite.form)
      * [Input form](#cite.form.in)
        * [Input form fields](#cite.form.in.fields)
      * [Output form](#cite.form.out)
* [Dependencies](#dependencies)
* [Demo](#demo)

This plugin builds a form for input for the `Cite` object.

# <a id="use" href="#use">Use</a>

After including the necessary files like below,
you can make a new `jQueryCite` object.

```html
<script type="text/javascript" src="path/to/jquery.js"></script>
<script type="text/javascript" src="path/to/citeproc.js"></script>
<script type="text/javascript" src="path/to/citation-0.2.js"></script>
<script type="text/javascript" src="path/to/jquery.citation-0.2.js"></script>
```

## <a id="cite" href="#cite">jQueryCite</a>

Make a new `jQueryCite` object like this:

```js
var example = new jQueryCite( <options> )
```

The options are:

1. `defaultOptions`: [Options](#citation.cite) to be passed to `Cite`
2. `saveInCookies`: Save data in cookies when `.save()`d
3. `add`: Callback to execute when data is submitted to collection
4. `inputForm` and `outputForm`: HTML template (see [docs](#jquery.form))

## <a name="form"><a id="cite.form" href="#cite.form">HTML templates</a></a>

Of course, you can include all sorts of things in the templates, but the following things are going to get used. Templates below are in [Jade/Pug](https://github.com/pugjs/pug). Elements may be wrapped in containers, but the general hierarchy should be like this

### <span name="form.in"><a id="cite.form.in" href="#cite.form.in">Input form</a></span>

```
.cjs-in
  .cjs-piece.cjs-input
    // List of fieldsets, see below
  .cjs-piece.cjs-import
    .cjs-import-name // Text input to hold input value names
    .cjs-import-file // File input
  .cjs-piece.cjs-preview
    .cjs-draft // Element holding draft
    .cjs-add // Submit (and clear) draft
    .cjs-delete // Clear draft
```

#### <a name="form.in.fields"><a id="cite.form.in.fields" href="#cite.form.in.fields">Input form fields</a></a>

Form fields consist of a `fieldset` element and inside an `input` element, with the following attributes:

* `fieldset`
  * `data-cjs-field-type`: For what publication types should this field be visible (omit when it should always be visible)
  * `data-cjs-field-state`: `"hidden"`, omitted or `"visible"`. Assigned by program
* `input`
  * `data-cjs-field`: Name of the corresponding CSL property. When CSL properties are complex, `jQueryCite` usually helps out
  * `type`: Usually `"text"`, but depends on CSL property. If it gives input to jQuery in the correct format, it's okay

Exceptions:

* The field or the `page` property should have two `input`s
* Fields `author`, `container-author`, `editor` and `publisher-title` get `.CJSMultipleInput()`, so multiple `input`s aren't necessary, as they're added dynamically
* One of the fields, preferably the first one, should be a `select` (`data-cjs-field="type"`), containing publication type options

### <a name="form.out"><a id="cite.form.out" href="#cite.form.out">Output form</a></a>

```
.cjs-out
  .cjs-piece.cjs-settings
    .cjs-opt
      fieldset
        select.cjs-type // HTML text or plain text
          option(value="html")
          option(value="string")
      fieldset
        select.cjs-style // Formatting style
          option(value="citation.apa")
          option(value="citation.vancouver")
          option(value="citation.harvard1")
          // Formatted citations can be expanded, if correct material is provided to Cite
          option(value="bibtex")
          option(value="csl")
      fieldset
        select.cjs-lan // Output language
          option(value="en-US")
          option(value="es-ES")
          option(value="du-DU")
          option(value="fr-FR")
          option(value="nl-NL")
          // Langs can be expanded, if correct material is provided to Cite
  .cjs-piece
    .cjs-output // Holds data
  .cjs-piece.cjs-export
    .cjs-export-copy // Copy data on click
    .cjs-export-save // Download data on click
```

# <a id="dependencies" href="#dependencies">Dependencies</a>

* [jQuery](https://jquery.org)
* [Citation.js](https://larsgw.github.io/citation.js)

# <a id="demo" href="demo">Demo</a>

* [Demo](https://larsgw.github.io/citation.js-form/demo/)