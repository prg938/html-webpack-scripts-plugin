Improve control over scripts generated by [Webpack](https://webpack.js.org/).

<img src="https://github.com/prg938/html-webpack-scripts-plugin/assets/7237762/fb07e6d3-3162-40fe-a3a9-b019bd9cb38b" width=180>

[![npm version](https://badge.fury.io/js/html-webpack-scripts-plugin.svg)](http://badge.fury.io/js/html-webpack-scripts-plugin)

## Introduction
[`html-webpack-plugin`](https://www.npmjs.com/package/html-webpack-plugin) will add scripts generated by [Webpack](https://webpack.js.org/) into generated HTML like<br>
`<script type="text/javascript" src="/bundle/vendor.0a78e31b5c440.js"></script>`  without need to include them manually. However it won't give you additional control. For example you can't set `defer` attribute or make them inline.

## Installation
```shell
npm install html-webpack-plugin --save-dev (Must be installed)
npm install html-webpack-scripts-plugin --save-dev
```

Usage
----------------------

Suppose you have two scripts generated by webpack: 
`vendor.0a78e31b5c440.js` 
`app.4234fe71c300ea.js` you can:

#### 1. Add specific attributes like `async` `defer` `id` `charset` or custom like `data-*`:
```js
// webpack.config.js
const HtmlWebpackScriptsPlugin = require('html-webpack-scripts-plugin')
const HtmlWebpackScriptsPluginInstance = new HtmlWebpackScriptsPlugin({
	'defer charset=utf-8': /vendor/,
	'async id=appscript data-script-defer=true': /app/
})
module.exports = {
	...
	plugins: [..., HtmlWebpackScriptsPluginInstance]
	...
} 
```
Output:
```html
<script defer charset="utf-8" type="text/javascript" src="vendor.0a78e31b5c440.js"></script>
<script async id="appscript" data-script-defer="true" type="text/javascript" src="app.4234fe71c300ea.js"></script>
```

#### 2. Make scripts inline:
```js
// vendor.0a78e31b5c440.js
console.log('Hi')

// app.4234fe71c300ea.js
console.log('Webpack')
```

```js

// webpack.config.js

const HtmlWebpackScriptsPlugin = require('html-webpack-scripts-plugin')
const HtmlWebpackScriptsPluginInstance = new HtmlWebpackScriptsPlugin({ inline: /vendor|app/ })
module.exports = {
	...
	plugins: [..., HtmlWebpackScriptsPluginInstance]
	...
}
```
Output:
```html
<script type="text/javascript">console.log('Hi')</script>
<script type="text/javascript">console.log('Webpack')</script>
```

#### Template extension:
By default `html-webpack-plugin` generates .html file. In case if it generates file with different extension you can specify extension manually: 

```js

const HtmlWebpackScriptsPlugin = require('html-webpack-scripts-plugin')
const HtmlWebpackScriptsPluginInstance = new HtmlWebpackScriptsPlugin({
	templateExtension: 'ext',
	inline: /\.js$/
})
 
```
