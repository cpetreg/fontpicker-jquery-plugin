# Fontpicker jQuery Plugin

A component to quickly choose fonts from Google Web Fonts, custom fonts you (the web developer) provide, as well as system fonts.
Lets users easily select and preview a font from Google's large range of free fonts, and optionally select a font weight and font style (normal or italics).
This plugin is the successor of the [Fontselect jQuery plugin](https://github.com/av01d/fontselect-jquery-plugin).

[See a live demo here](https://av01d.github.io/fontpicker-jquery-plugin/index.html).

## Table of contents
- [Features](#features)
- [Demo](#demo)
- [Getting started](#getting-started)
- [Options](#options)
- [Methods](#methods)
- [Events](#events)
- [Real World Examples](#real-world-examples)
- [License](#license)

## Features

- Quickly preview and select any Google font family.
- Optionally present system and local fonts (`.woff`) as well.
- Optionally choose font weight and font style.
- Find fonts by name, language and category (serif, sans-serif, display, handwriting, monospace).
- Users can favor fonts (favorites are stored in a cookie), allowing them to quickly find them a next time.
- Editable sample text (default: *The quick brown fox jumps over the lazy dog*)
- Keyboard navigation
  - `Up/Down` cursor keys navigate through options.
  - `Enter` key selects on option, double-clicking does too.
  - `Esc` closes the picker.
- Drop-in replacement for a regular input element.

## Demo

[Live demo](https://av01d.github.io/fontpicker-jquery-plugin/index.html).

## Getting started

### Installation

```html
<link href="/path/to/dist/jquery.fontpicker.min.css" rel="stylesheet">
<script src="https://code.jquery.com/jquery-3.4.1.slim.min.js"></script>
<script src="/path/to/dist/jquery.fontpicker.min.js"></script>
```
### Usage

To create a font picker, simply run the plugin on a standard html `input` element.

#### Syntax
```js
$('input.fonts').fontpicker([options]);
````

- **options** (optional)
  - Type: `Object`
  - The options for the font picker. See available [options](#options).

#### Example

```html
<input class="fonts">
```

```js
$('input.fonts').fontpicker({
   lang: 'en',
   variants: true,
   lookahead: 2,
   googleFonts: 'Alegreya,Boogaloo,Coiny,Dosis,Emilys Candy,Faster One,Galindo'.split(','),
   localFonts: {
      "Arial": {
         "category": "sans-serif",
         "variants": "400,400i,600,600i"
      },
      "Georgia": {
         "category": "serif",
         "variants": "400,400i,600,600i"
      },
      "Times New Roman": {
         "category": "serif",
         "variants": "400,400i,600,600i"
      },
      "Verdana": {
         "category": "sans-serif",
         "variants": "400,400i,600,600i",
      },
      "Action Man": {},
      "Bauer": {
         "category": "display",
         "variants": "400,400i,600,600i",
         "subsets": "latin-ext,latin"
      },
      "Bubble": {
         "category": "display",
         "variants": "400,400i,600,600i",
         "subsets": "latin-ext,latin"
      }
   },
   localFontsUrl: 'fonts/' // End with a slash!
});
````

When a user picks a font, the original `input` element will be filled with the chosen font family name: `Alegreya`, `Arial`, `Faster One` etc.
If the `variants` option has been enabled (it is by default), the font family will be followed by a font-weight and an italics indicator.
Some examples:

- `Alegreya:400`: Font family `Alegreya`, font weight `400`
- `Alegreya:700`: Font family `Alegreya`, font weight `700`
- `Alegreya:700i`: Font family `Alegreya`, font weight `700`, italics
- `Faster One:400`: Font family `Faster One`, font weight `400`
- `Arial:600i`: Font family `Arial`, font weight `600`, italics

[⬆ back to top](#table-of-contents)

## Options

Fontpicker has one argument, an options object that you can customise.

### lang

- Type: `String`
- Default: `en`
- Options:
  - `en`: English
  - `de`: German
  - `nl`: Dutch

The interface language.
If you need a translation in another language: take a look at the `dictionaries` variable in `jquery.fontpicker.js`, and send me the translations for your language.

### variants

- Type: `Boolean`
- Default: `true`

With `variants: true`, users can not only select a font family, but the variant (font weight and font style) of it as well, if applicable. Many fonts in the Google Repository have multiple variants (multiple font weights, normal and italic styles).
In this case, the `input` element will have a value that consists of the chosen font, followed by the font-weight and an italics indicator (see [Example](#example)).

### lookahead

- Type: `Number`, `Boolean`
- Default: 0
- Options: Any positive number, or `false`

A number of fonts to preload ahead in the list. Default: `0`. Use `false` to disable fonts preloading.
When the user scrolls the font list, each font is rendered in its own font family. This is accomplished by loading the external font on demand, as soon as the font becomes visible in the list. The `lookahead` indicates how many not-yet-visible fonts will be loaded in advance.
Use `false` to disable preloading of fonts: fonts in the list will no longer be rendered in their own font family.

### googleFonts

- Type: `Array`
- Default: All available Google Fonts

An array of Google fonts to present in the font list. Shows all available Google fonts by default. Use `false` to not show Google Fonts at all.

### localFonts

The Google Fonts Repository doesn't always offer enough options. The fontpicker plugin allows you to presentcustom fonts as well.
The local font files have to be in `.woff` (not `.ttf`) format (for best compatibility with as many browsers as possible), and they should all be put in a single folder, under the document root folder of your site. Something like `/fonts/` makes sense.
Provide the path to this folder as the `localFontsUrl` configuration parameter.
You can convert `.otf/.ttf` fonts to `.woff` on [transfonter.org](https://transfonter.org/).

- Type: `Object`
- Default:
  ```
   "Arial": {
      "category": "sans-serif",
      "variants": "400,400i,600,600i"
   },
   "Courier New": {
      "category": "monospace",
      "variants": "400,400i,600,600i"
   },
   "Georgia": {
      "category": "serif",
      "variants": "400,400i,600,600i"
   },
   "Tahoma": {
      "category": "sans-serif",
      "variants": "400,400i,600,600i"
   },
   "Times New Roman": {
      "category": "serif",
      "variants": "400,400i,600,600i"
   },
   "Trebuchet MS": {
      "category": "sans-serif",
      "variants": "400,400i,600,600i"
   },
   "Verdana": {
      "category": "sans-serif",
      "variants": "400,400i,600,600i",
   }
   ```

The key of an item is the *font family*. As mentioned above, make sure that custom (non-system) fonts are available on your webserver, as `.woff` files. Make sure the name of the font files matches the *font family* name used here:
`"Action Man"` -> `/fonts/Action Man.woff`
`"Bubble"` -> `/fonts/Bubble.woff`

The value of an item is an object, containing up to 3 properties:
- `category`: A `String`, containing one of `serif, sans-serif, display, handwriting, monospace`. This allows users to filter fonts by category. If omitted, the font is listed under the `other` category.
- `variants`: A `String`, containing a comma-separated list of variants available for the font. See example below. If omitted, users cannot pick a variant for this font (the font weight will be `400`, the font style will be `normal` (non italics)).
- `subsets`: A `String`, containing a comma-separated list of language-subsets the font entails. This allows users to filter fonts by language. If omitted, the font can (only) be found under `All languages`.

Example:
```
{
   "Arial": {
      "category": "sans-serif",
      "variants": "400,400i,600,600i"
   },
   "Georgia": {
      "category": "serif",
      "variants": "400,400i,600,600i"
   },
   "Times New Roman": {
      "category": "serif",
      "variants": "400,400i,600,600i"
   },
   "Verdana": {
      "category": "sans-serif",
      "variants": "400,400i,600,600i",
   },
   "Action Man": {},
   "Bauer": {
      "category": "display",
      "variants": "400,400i,600,600i",
      "subsets": "latin-ext,latin"
   },
   "Bubble": {
      "category": "display",
      "variants": "400,400i,600,600i",
      "subsets": "latin-ext,latin"
   }
};
```

### localFontsUrl

- Type: `String`
- Default: `/fonts/`

Path to folder where local fonts are stored (in .woff format). Default: `/fonts/`. *Make sure to end with a slash!*

### parentElement

- Type: `String` or `jQuery object`
- Default: `'body'`

Parent element (jQuery selector/element) to attach the font picker to. The default `body` should suffice in pretty much all cases. Only tinker with this if you know what you're doing.

### debug

- Type: `Boolean`
- Default: `false`

When enabled, the plugin shows info about fonts being loaded in the console.

[⬆ back to top](#table-of-contents)

## Methods

### set font

Programmatically select a font by calling `val()` on the original input element, then triggering the `change` event:
```
// Select 'Geo' font family
$('#font').val('Geo').trigger('change');
```
or
```
// Select 'Orbitron' font family, weight 900
$('#font').val('Orbitron:900').triggger('change');
```
or
```
// Select 'Open Sans' font family, weight 800, italics
$('#font').val('Open Sans:800i').triggger('change');
```

### show

Show the font picker manually
```
$('#font').fontpicker('show');
```

### hide

Hide the font picker manually
```
$('#font').fontpicker('hide');
```

### destroy

Destroy the font picker, revert element back to original.
```
$('#font').fontpicker('destroy');
```

[⬆ back to top](#table-of-contents)

## Events

Fontpicker triggers the `change` event on the original `input` element when a font is selected.
See this example for how this could be used to update the font on the current page.

```html
<input id="font">
```

```js
$('#font').fontpicker().on('change', function() {
   // Split font into family and weight/style
   var tmp = this.value.split(':'),
      family = tmp[0],
      variant = tmp[1] || '400',
      weight = parseInt(variant,10),
      italic = /i$/.test(variant);

   // Set selected font on body
   var css = {
      fontFamily: "'" + family + "'",
      fontWeight: weight,
      fontStyle: italic ? 'italic' : 'normal'
   };

   console.log(css);
   $('body').css(css);
});
```

[⬆ back to top](#table-of-contents)

## Real World Examples

The Fontpicker plugin is used (among others) on the following websites:

- [PhotoEditor.com](https://www.photoeditor.com/)
- [PhotoFilters.com](https://www.photofilters.com/)
- [PhotoResizer.com](https://www.photoresizer.com/)
- [PrintScreenshot.com](https://www.printscreenshot.com/)

## License

This plugin is released under the MIT license. It is simple and easy to understand and places almost no restrictions on what you can do with the code.
[More Information](http://en.wikipedia.org/wiki/MIT_License)

The development of this plugin was funded by [Zygomatic](https://www.zygomatic.nl/).

[⬆ back to top](#table-of-contents)
