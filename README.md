<p align="center">
	<a href="http://lindell.me/JsBarcode"><img src="http://lindell.me/JsBarcode/other/logo.svg" alt="JsBarcode"/></a>
	<br><br>
	<a href="http://travis-ci.org/lindell/JsBarcode"><img src="https://secure.travis-ci.org/lindell/JsBarcode.svg" alt="Build Status"/></a>
	<a href="https://scrutinizer-ci.com/g/lindell/JsBarcode/?branch=master"><img src="https://scrutinizer-ci.com/g/lindell/JsBarcode/badges/quality-score.png?b=master" alt="Scrutinizer Code Quality"/></a>
	<a href="https://www.jsdelivr.com/package/npm/jsbarcode"><img src="https://data.jsdelivr.com/v1/package/npm/jsbarcode/badge?style=rounded" alt="CDN"></a>
	<a href="https://github.com/lindell/JsBarcode/blob/master/MIT-LICENSE.txt"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"/></a>
</p>

Introduction
----
**CodeScanner** provides a JavaScript-based **QR code and barcode scanner** that can be easily integrated into any **HTML-based** webpage. It supports scanning using the camera on both HTTPS and localhost environments, while also working on HTTP (though HTTP does not support camera access due to security reasons).

Demo
----
#### [Demo #1](https://tihloh.github.io/codescanner/demo1.html)
#### [Demo #2](https://tihloh.github.io/codescanner/demo2.html)

Features:
----
* QR Code Scanning: Quickly scan and decode QR codes.
* Barcode Scanning: Supports various barcode formats.
* Camera Access: Utilizes the device's camera for scanning (HTTPS and localhost only).
* Cross-Browser Compatibility: Works on major browsers that support camera access.
* Two Modes:
  * External Mode: Open scanner in a new window on button click.
  * Embedded Mode: Embed scanner within the page using an iframe with continuous multiple scanning capability.



Examples for browsers:
----

#### First create a canvas (or image)
````html
<svg id="barcode"></svg>
<!-- or -->
<canvas id="barcode"></canvas>
<!-- or -->
<img id="barcode"/>
````



#### Simple example:
````javascript
JsBarcode("#barcode", "Hi!");
// or with jQuery
$("#barcode").JsBarcode("Hi!");
````

##### Result:
![Result](https://s3-eu-west-1.amazonaws.com/js-barcode/barcodes/simple.svg)


#### Example with options:
````javascript
JsBarcode("#barcode", "1234", {
  format: "pharmacode",
  lineColor: "#0aa",
  width:4,
  height:40,
  displayValue: false
});
````
##### Result:
![Result](https://s3-eu-west-1.amazonaws.com/js-barcode/barcodes/advanced.svg)


#### More advanced use case:
````javascript
JsBarcode("#barcode")
  .options({font: "OCR-B"}) // Will affect all barcodes
  .EAN13("1234567890128", {fontSize: 18, textMargin: 0})
  .blank(20) // Create space between the barcodes
  .EAN5("12345", {height: 85, textPosition: "top", fontSize: 16, marginTop: 15})
  .render();
````
##### Result:
![Result](https://s3-eu-west-1.amazonaws.com/js-barcode/barcodes/simple.svg)



#### Or define the value and options in the HTML element:
Use any `jsbarcode-*` or `data-*` as attributes where `*` is any option.
````html
<svg class="barcode"
  jsbarcode-format="upc"
  jsbarcode-value="123456789012"
  jsbarcode-textmargin="0"
  jsbarcode-fontoptions="bold">
</svg>
````

And then initialize it with:
````javascript
JsBarcode(".barcode").init();
````

##### Result:
![Result](https://s3-eu-west-1.amazonaws.com/js-barcode/barcodes/init.svg)



#### Retrieve the barcode values so you can render it any way you'd like
Pass in an object which will be filled with data.
```javascript
const data = {};
JsBarcode(data, 'text', {...options});
```
data will be filled with a ``` encodings ``` property which has all the needed values.
See wiki for an example of what data looks like.


Setup for browsers:
----
### Step 1:
Download or get the CDN link to the script:

| Name | Supported barcodes | Size (gzip) | CDN / Download |
|------|--------------------|:-----------:|---------------:|
|  *All*  |  *All the barcodes!*  |  *10.1 kB*  |  *[JsBarcode.all.min.js][1]*  |
|  CODE128  |  CODE128 (auto and force mode)  |  6.2 kB  |  [JsBarcode.code128.min.js][2]  |
|  CODE39  |  CODE39  |  5.1 kB  |  [JsBarcode.code39.min.js][3]  |
|  EAN / UPC  |  EAN-13, EAN-8, EAN-5, EAN-2, UPC (A)  |  6.6 kB  |  [JsBarcode.ean-upc.min.js][4]  |
|  ITF  |  ITF, ITF-14  |  5 kB  |  [JsBarcode.itf.min.js][5]  |
|  MSI  |  MSI, MSI10, MSI11, MSI1010, MSI1110  |  5 kB  |  [JsBarcode.msi.min.js][6]  |
|  Pharmacode  |  Pharmacode  |  4.7 kB  |  [JsBarcode.pharmacode.min.js][7]  |
|  Codabar  |  Codabar  |  4.9 kB  |  [JsBarcode.codabar.min.js][8]  |


### Step 2:
Include the script in your code:


````html
<script src="JsBarcode.all.min.js"></script>
````

### Step 3:
You are done! Go generate some barcodes :smile:

Bower and npm:
----
You can also use [Bower](http://bower.io) or [npm](https://www.npmjs.com) to install and manage the library.
````bash
bower install jsbarcode --save
````
````bash
npm install jsbarcode --save
````

Node.js:
----

#### With canvas:
```` javascript
var JsBarcode = require('jsbarcode');

// Canvas v1
var Canvas = require("canvas");
// Canvas v2
var { createCanvas } = require("canvas");

// Canvas v1
var canvas = new Canvas();
// Canvas v2
var canvas = createCanvas();

JsBarcode(canvas, "Hello");

// Do what you want with the canvas
// See https://github.com/Automattic/node-canvas for more information
````

#### With svg:
```` javascript
const { DOMImplementation, XMLSerializer } = require('xmldom');
const xmlSerializer = new XMLSerializer();
const document = new DOMImplementation().createDocument('http://www.w3.org/1999/xhtml', 'html', null);
const svgNode = document.createElementNS('http://www.w3.org/2000/svg', 'svg');

JsBarcode(svgNode, 'test', {
    xmlDocument: document,
});

const svgText = xmlSerializer.serializeToString(svgNode);
````


Options:
----
For information about how to use the options, see [the wiki page](https://github.com/lindell/JsBarcode/wiki/Options).

| Option | Default value | Type |
|--------|---------------|------|
| [`format`](https://github.com/lindell/JsBarcode/wiki/Options#format) | `"auto" (CODE128)` | `String` |
| [`width`](https://github.com/lindell/JsBarcode/wiki/Options#width) | `2` | `Number` |
| [`height`](https://github.com/lindell/JsBarcode/wiki/Options#height) | `100` | `Number` |
| [`displayValue`](https://github.com/lindell/JsBarcode/wiki/Options#display-value) | `true` | `Boolean` |
| [`text`](https://github.com/lindell/JsBarcode/wiki/Options#text) | `undefined` | `String` |
| [`fontOptions`](https://github.com/lindell/JsBarcode/wiki/Options#font-options) | `""` | `String` |
| [`font`](https://github.com/lindell/JsBarcode/wiki/Options#font) | `"monospace"` | `String` |
| [`textAlign`](https://github.com/lindell/JsBarcode/wiki/Options#text-align) | `"center"` | `String` |
| [`textPosition`](https://github.com/lindell/JsBarcode/wiki/Options#text-position) | `"bottom"` | `String` |
| [`textMargin`](https://github.com/lindell/JsBarcode/wiki/Options#text-margin) | `2` | `Number` |
| [`fontSize`](https://github.com/lindell/JsBarcode/wiki/Options#font-size) | `20` | `Number` |
| [`background`](https://github.com/lindell/JsBarcode/wiki/Options#background)  | `"#ffffff"` | `String (CSS color)` |
| [`lineColor`](https://github.com/lindell/JsBarcode/wiki/Options#line-color) | `"#000000"` | `String (CSS color)` |
| [`margin`](https://github.com/lindell/JsBarcode/wiki/Options#margins) | `10` | `Number` |
| [`marginTop`](https://github.com/lindell/JsBarcode/wiki/Options#margins) | `undefined` | `Number` |
| [`marginBottom`](https://github.com/lindell/JsBarcode/wiki/Options#margins) | `undefined` | `Number` |
| [`marginLeft`](https://github.com/lindell/JsBarcode/wiki/Options#margins) | `undefined` | `Number` |
| [`marginRight`](https://github.com/lindell/JsBarcode/wiki/Options#margins) | `undefined` | `Number` |
| [`valid`](https://github.com/lindell/JsBarcode/wiki/Options#valid) | `function(valid){}` | `Function` |

Contributions and feedback:
----
We :heart: contributions and feedback.

If you want to contribute, please check out the [CONTRIBUTING.md](https://github.com/lindell/JsBarcode/blob/master/CONTRIBUTING.md) file.

If you have any question or suggestion [create an issue](https://github.com/lindell/JsBarcode/issues/new) or ask about it in the [gitter chat](https://gitter.im/lindell/JsBarcode).

Bug reports should always be done with a [new issue](https://github.com/lindell/JsBarcode/issues/new).

License:
----
JsBarcode is shared under the [MIT license](https://github.com/lindell/JsBarcode/blob/master/MIT-LICENSE.txt). This means you can modify and use it however you want, even for comercial use. But please give this the Github repo a :star: and write a small comment of how you are using JsBarcode in the [gitter chat](https://gitter.im/lindell/JsBarcode).



[1]: https://cdn.jsdelivr.net/npm/jsbarcode@3.11.0/dist/JsBarcode.all.min.js "jsdelivr all barcodes"
[2]: https://cdn.jsdelivr.net/npm/jsbarcode@3.11.0/dist/barcodes/JsBarcode.code128.min.js "jsdelivr code128"
[3]: https://cdn.jsdelivr.net/npm/jsbarcode@3.11.0/dist/barcodes/JsBarcode.code39.min.js "jsdelivr code39"
[4]: https://cdn.jsdelivr.net/npm/jsbarcode@3.11.0/dist/barcodes/JsBarcode.ean-upc.min.js "jsdelivr ean/upc"
[5]: https://cdn.jsdelivr.net/npm/jsbarcode@3.11.0/dist/barcodes/JsBarcode.itf.min.js "jsdelivr itf"
[6]: https://cdn.jsdelivr.net/npm/jsbarcode@3.11.0/dist/barcodes/JsBarcode.msi.min.js "jsdelivr msi"
[7]: https://cdn.jsdelivr.net/npm/jsbarcode@3.11.0/dist/barcodes/JsBarcode.pharmacode.min.js "jsdelivr pharmacode"
[8]: https://cdn.jsdelivr.net/npm/jsbarcode@3.11.0/dist/barcodes/JsBarcode.codabar.min.js "jsdelivr codabar"
