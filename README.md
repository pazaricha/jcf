# JCF - JavaScript Custom Forms
This library allows crossbrowser customization of form elements using CSS.

Check [live demo](http://w3co.github.io/jcf/).

## Browser support
The script was tested in the following browsers:

 - Internet Explorer 8+
 - Firefox
 - Chrome
 - Safari
 - Opera
 - Windows 8+ Touch desktops
 - Windows Phone 8+
 - Android 4+
 - iOS7+

## Usage
The script requires [jQuery 1.7+](http://jquery.com/) to work properly. To add script in your page simply attach core file - `jcf.js` and some of modules you want to use for customization:</p>

```html
<script src="js/jquery.js"></script>
<script src="js/jcf.js"></script>
<script src="js/jcf.select.js"></script>
<script src="js/jcf.radio.js"></script>
<script src="js/jcf.checkbox.js"></script>
```

When the page is loaded all you have to do is simply call function:

```js
$(function() {
	jcf.replaceAll();
});
```

## General API Information

Global `jcf` object has several methods to control custom form elements on the page:

`jcf.replaceAll( [context] )` - Replace elements on the whole page. Optional argument is context to use (can be CSS selector, or DOM/jQuery object).

`jcf.replace( elements [, moduleName] [, customOptions] )` - Replace certain element or multiple elements. Returns custom form element instance. The first argument is CSS selector, or DOM/jQuery object to be customized. Second argument is optional and used to specify module which should be used for customization. By default it is `false` which will result module to be auto detected. Third argument is module options which can be specified with object.

`jcf.destroyAll( [context] )` - Destroy all custom form elements instances and restore original form elements. Optional argument is context to use (can be CSS selector, or DOM/jQuery object).

`jcf.destroy( elements )` - Destroy certain element or multiple form elements. Should be applied to native form controls.

`jcf.refreshAll( [context] )` - Redraw all custom form instances. Should be used when values of form elements are modified by other scripts. Optional argument is context to use (can be CSS selector, or DOM/jQuery object).

`jcf.refresh( elements )` - Refresh certain element or multiple form elements.

## Getting the instance of customized form element
In any time it's possible to get instance of customized form element. Use method `jcf.getInstance` to do this:

```javascript
var countrySelect = document.getElementById('country-select');
var customFormInstance = jcf.getInstance(countrySelect);

customFormInstance.refresh();
```

## Setting Options

There are two ways of specifying options for modules - override module defaults and specify options per element.

```javascript
// set options for Checkbox module
jcf.setOptions('Checkbox', {
	checkedClass: 'test',
	wrapNative: false
});

// replace all form elements with modified default options
jcf.replaceAll();
```

The second way is to specify options for certain element in HTML:
``` html
<input type="checkbox" data-jcf='{"checkedClass": "test", "wrapNative": false}'>
```
*(Please be careful and use valid JSON)*

## Module Options

Each module has options. Some of options are common between modules and some are unique. The most commonly used options in modules are listed below.

### Select

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
			<th>Data Type</th>
			<th>Default</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>wrapNative</code></td>
			<td>Wrap native select inside fake area, so that native dropdown will be shown</td>
			<td>boolean</td>
			<td><code>true</code></td>
		</tr>
		<tr>
			<td><code>wrapNativeOnMobile</code></td>
			<td>Show native dropdown on mobile devices even if <code>wrapNative</code> is <code>false</code></td>
			<td>boolean</td>
			<td><code>true</code></td>
		</tr>
		<tr>
			<td><code>fakeDropInBody</code></td>
			<td>Active only when custom dropdown is used. Specifies where to append custom dropdown - in document root, or inside select area</td>
			<td>boolean</td>
			<td><code>true</code></td>
		</tr>
		<tr>
			<td><code>useCustomScroll</code></td>
			<td>Use custom scroll inside custom dropdown if <code>Scrollable</code> module present</td>
			<td>boolean</td>
			<td><code>true</code></td>
		</tr>
		<tr>
			<td><code>flipDropToFit</code></td>
			<td>Flip custom dropdown if it does not fit in viewport</td>
			<td>boolean</td>
			<td><code>true</code></td>
		</tr>
		<tr>
			<td><code>maxVisibleItems</code></td>
			<td>How many options should be visible in dropdown before scrollbar appears</td>
			<td>number</td>
			<td><code>10</code></td>
		</tr>
	</tbody>
</table>

### Checkbox

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
			<th>Data Type</th>
			<th>Default</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>wrapNative</code></td>
			<td>Wrap native checkbox inside fake area for better compatibility with event handlers attached by other scripts</td>
			<td>boolean</td>
			<td><code>true</code></td>
		</tr>
		<tr>
			<td><code>checkedClass</code></td>
			<td>Specify class which will be added to fake area when checkbox is checked</td>
			<td>string</td>
			<td><code>"jcf-checked"</code></td>
		</tr>
		<tr>
			<td><code>labelActiveClass</code></td>
			<td>Specify class which will be added to corresponding <code>&lt;label&gt;</code> when checkbox is checked</td>
			<td>string</td>
			<td><code>"jcf-label-active"</code></td>
		</tr>
	</tbody>
</table>

### Radio

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
			<th>Data Type</th>
			<th>Default</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>wrapNative</code></td>
			<td>Wrap native radio inside fake area for better compatibility with event handlers attached by other scripts</td>
			<td>boolean</td>
			<td><code>true</code></td>
		</tr>
		<tr>
			<td><code>checkedClass</code></td>
			<td>Specify class which will be added to fake area when radio is checked</td>
			<td>string</td>
			<td><code>"jcf-checked"</code></td>
		</tr>
		<tr>
			<td><code>labelActiveClass</code></td>
			<td>Specify class which will be added to corresponding <code>&lt;label&gt;</code> when radio is checked</td>
			<td>string</td>
			<td><code>"jcf-label-active"</code></td>
		</tr>
	</tbody>
</table>

### File

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
			<th>Data Type</th>
			<th>Default</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>buttonText</code></td>
			<td>Specify default text for upload button (its better to specify this option from HTML for proper localization).</td>
			<td>string</td>
			<td><code>"Choose file"</code></td>
		</tr>
		<tr>
			<td><code>placeholderText</code></td>
			<td>Specify default text for input when no file is selected (its better to specify this option from HTML for proper localization)</td>
			<td>string</td>
			<td><code>"No file chosen"</code></td>
		</tr>
	</tbody>
</table>

### Scrollable

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
			<th>Data Type</th>
			<th>Default</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>handleResize</code></td>
			<td>Handle resize events so that scrollable area will be responsive</td>
			<td>boolean</td>
			<td><code>true</code></td>
		</tr>
		<tr>
			<td><code>alwaysShowScrollbars</code></td>
			<td>Always show scrollbars event if they cant scroll anything</td>
			<td>boolean</td>
			<td><code>false</code></td>
		</tr>
		<tr>
			<td><code>alwaysPreventMouseWheel</code></td>
			<td>Always prevent mouse wheel scrolling when its used over scrollable element. This way page wont be scrolled even if scrollable area is at the scrolled to the top/bottom.</td>
			<td>boolean</td>
			<td><code>false</code></td>
		</tr>
	</tbody>
</table>

### Textarea

Apply custom scrollbar on `<textarea>` (Works only when `Scrollable` module is available).

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
			<th>Data Type</th>
			<th>Default</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>resize</code></td>
			<td>Add resize grip to <code>&lt;textarea&gt;</code></td>
			<td>boolean</td>
			<td><code>true</code></td>
		</tr>
	</tbody>
</table>

## License

This script is licensed under the [MIT License](LICENSE.txt).

Copyright 2014 [PSD2HTML.com](http://psd2html.com/?jcf)