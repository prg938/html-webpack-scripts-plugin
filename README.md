
`html-webpack-scripts-plugin` is a plugin for [Webpack](https://webpack.js.org/).

## Why
By default Webpack will generate plain scripts like `vendor.0a78e31b5c440.js`. In order to serve these script assets and other generated assets by Webpack (like stylesheets) you should have index.html file and include those assets manually or a plugin that generates HTML and includes those assets automatically, like [`html-webpack-plugin`](https://www.npmjs.com/package/html-webpack-plugin).
More likely you'll use the second option and generate HTML automatically.

However [`html-webpack-plugin`](https://www.npmjs.com/package/html-webpack-plugin) will add plain scripts into generated HTML like
`<script type="text/javascript" src="/bundle/vendor.0a78e31b5c440.js"></script>`. It won't give you additional control over those scripts.
But if you want to get additional control over those scripts `html-webpack-scripts-plugin` will help!

Usage
----------------------
#### Add specific attributes like `async` `defer` `id` `charset`:

Suppose we have two script assets generated by webpack: `vendor.0a78e31b5c440.js` `app.4234fe71c300ea.js`.
Lets add specific attributes to them:
```js
// webpack.config.js
plugins: [
  new HtmlWebpackScriptsPlugin({
    'defer charset=utf8': /vendor/,
    'async id=appscript': /app/
  })
]
```

And these scripts will be included in your HTML:
```html
<script defer charset="utf8" type="text/javascript" src="vendor.0a78e31b5c440.js"></script>
<script async id="appscript" type="text/javascript" src="app.4234fe71c300ea.js"></script>
```

#### Add custom attributes like `data-*`
```js
```

#### Make scripts inline:
Suppose we have two script assets generated by webpack `vendor.0a78e31b5c440.js` `app.4234fe71c300ea.js`
```js
// vendor.0a78e31b5c440.js
var helloWebpack = 'hello webpack'
console.log(helloWebpack)
```
```js
// app.4234fe71c300ea.js
var helloApp = 'Hello app'
console.log(helloApp)
```

Lets make them inline:
```js
plugins: [
  new HtmlWebpackScriptsPlugin({ inline: /vendor/ })
]
```

And these scripts will be included in your HTML:
```html
<script type="text/javascript">
var helloWebpack = 'hello webpack'
console.log(helloWebpack)
</script>

<script type="text/javascript">
var helloApp = 'Hello app'
console.log(helloApp)
</script>

```
