Include Assets extension for the HTML Webpack Plugin
========================================
[![npm version](https://badge.fury.io/js/html-webpack-include-assets-plugin.svg)](https://badge.fury.io/js/html-webpack-include-assets-plugin) [![Build Status](https://travis-ci.org/jharris4/html-webpack-include-assets-plugin.svg?branch=master)](https://travis-ci.org/jharris4/html-webpack-include-assets-plugin) [![js-semistandard-style](https://img.shields.io/badge/code%20style-semistandard-brightgreen.svg?style=flat-square)](https://github.com/Flet/semistandard)

Enhances [html-webpack-plugin](https://github.com/ampedandwired/html-webpack-plugin)
functionality by allowing you to specify js or css assets to be included.

When using a plugin such as [copy-webpack-plugin](https://github.com/kevlened/copy-webpack-plugin) you may have assets output to your build directory that are not detected/output by the html-webpack-plugin.

This plugin allows you to force some of these assets to be included in the output from html-webpack-plugin.

Installation
------------
You must be running webpack on node 0.12.x or higher

Install the plugin with npm:
```shell
$ npm install --save-dev html-webpack-include-assets-plugin
```


Basic Usage
-----------
Require the plugin in your webpack config:

```javascript
var HtmlWebpackIncludeAssetsPlugin = require('html-webpack-include-assets-plugin');
```

Add the plugin to your webpack config as follows:

```javascript
plugins: [
  new HtmlWebpackPlugin(),
  new HtmlWebpackIncludeAssetsPlugin({ assets: [], append: true })
]  
```

Options
-------
The available options are:

- `assets`: `string` or `array`
  
  Assets that will be output into your html-webpack-plugin template. 

  Only assets ending in `.js` or `.css` are supported. The presence of assets that do not end in these extensions will cause an error.

- `append`: `boolean`

  Specifying whether the assets should be prepended (`false`) before any existing assets, or appended (`true`) after them.

- `publicPath`: `boolean` or `string`

  Specifying whether the assets should be prepended with webpack's public path or a custom publicPath (`string`).
  
  A value of `false` may be used to disable prefixing with webpack's publicPath, or a value like `myPublicPath/` may be used to prefix all assets with the given string. Default is `true`.

- `hash`: `boolean`

  Specifying whether the assets should be appended with webpack's compilation hash. This is useful for cache busting. Default is `false`.

Example
-------
Using `HtmlWebpackIncludeAssetsPlugin` and `CopyWebpackPlugin` to include assets to `html-webpack-plugin` template :

```javascript
plugins: [
  new CopyWebpackPlugin([
    { from: 'node_modules/bootstrap/dist/css', to: 'css/'},
    { from: 'node_modules/bootstrap/dist/fonts', to: 'fonts/'}
  ]),
  new HtmlWebpackPlugin(),
  new HtmlWebpackIncludeAssetsPlugin({
    assets: ['css/bootstrap.min.css', 'css/bootstrap-theme.min.css'],
    append: false
  })
]  
```

Appending and prepending at the same time :

```javascript
plugins: [
  new CopyWebpackPlugin([
    { from: 'node_modules/bootstrap/dist/css', to: 'css/'},
    { from: 'node_modules/bootstrap/dist/fonts', to: 'fonts/'}
  ]),
  new HtmlWebpackPlugin(),
  new HtmlWebpackIncludeAssetsPlugin({
    assets: ['css/bootstrap.min.css', 'css/bootstrap-theme.min.css'],
    append: false
  }),
  new HtmlWebpackIncludeAssetsPlugin({
    assets: ['css/custom.css'],
    append: true
  })
]
```

Using custom `publicPath` :

```javascript
plugins: [
  new CopyWebpackPlugin([
    { from: 'node_modules/bootstrap/dist/css', to: 'css/'},
    { from: 'node_modules/bootstrap/dist/fonts', to: 'fonts/'}
  ]),
  new HtmlWebpackPlugin(),
  new HtmlWebpackIncludeAssetsPlugin({
    assets: ['css/bootstrap.min.css', 'css/bootstrap-theme.min.css'],
    append: false,
    publicPath: 'myPublicPath/'
  })
]
```

Using `hash` option :

```javascript
plugins: [
  new CopyWebpackPlugin([
    { from: 'node_modules/bootstrap/dist/css', to: 'css/'},
    { from: 'node_modules/bootstrap/dist/fonts', to: 'fonts/'}
  ]),
  new HtmlWebpackPlugin(),
  new HtmlWebpackIncludeAssetsPlugin({
    assets: ['css/bootstrap.min.css', 'css/bootstrap-theme.min.css'],
    append: false,
    hash: true
  })
]
```
