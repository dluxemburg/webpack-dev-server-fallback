# webpack-dev-server-fallback

Use a static directory as a fallback for requests to webpack-dev-server when the build isn't ready. 

Useful in conjunction with [HtmlWebpackPlugin](https://github.com/jantimon/html-webpack-plugin) to avoid blank screens and timeouts.

## Install

`npm install gist:e75c23f911684110632f14b3229c7793 --save` (magic!)

## Use

In such as `webpack.config.js`:

```js
const webpackDevServerFallback = require('webpack-dev-server-fallback');

module.exports = {
  devServer: {
    before: webpackDevServerFallback()
  }
};
```

`webpackDevServerFallback` takes an `options` object with two properties:
  - **`wait`**: milliseconds to wait for build to be ready before serving fallback (default: 300)
  - **`directory`**: source for fallback files (default: "fallback", is passed to [`express.static`](https://expressjs.com/en/starter/static-files.html))
 
If you have other business to conduct with [`devServer.before`](https://webpack.js.org/configuration/dev-server#devserverbefore):
 
 ```js
module.exports = {
  devServer: {
    before(app, server) {
      // ...code, code, code
      webpackDevServerFallback()(app, server);
    }
  }
};
```