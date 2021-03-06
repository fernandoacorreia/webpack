[![webpack](http://webpack.github.io/assets/logo.png)](http://webpack.github.io)

[![NPM version](https://badge.fury.io/js/webpack.png)](http://badge.fury.io/js/webpack)

[documentation](http://webpack.github.io/docs/?utm_source=github&utm_medium=readme&utm_campaign=top)

# Introduction

webpack is a bundler for modules. The main purpose is to bundle javascript files for usage in browser.

**TL;DR**

* bundles [CommonJs](http://www.commonjs.org/specs/modules/1.0/) and [AMD](https://github.com/amdjs/amdjs-api/wiki/AMD) modules. (even combined)
* can create a single bundle or a bunch of chunks loaded on demand, to reduce initial loading time.
* dependencies are resolved while compiling, this makes the runtime very small
* loader can preprocess files while compiling, i. e. coffee-script to javascript

Check the [documentation](http://webpack.github.io/docs/?utm_source=github&utm_medium=readme&utm_campaign=trdr) if you want to know more...



# Examples

Take a look at the [`examples`](https://github.com/webpack/webpack/tree/master/examples) folder.



# Features

## Plugins

webpack has a rich plugin interface. Most of the features are internal plugins using this interface. This makes webpack very **flexible**.

## Performance

webpack uses async I/O and has multiple caching levels. This makes webpack fast and incredible **fast** on incremental compilation.

## Loaders

webpack allows to use loaders to preprocess files. This allows you to bundle **any static resource** not only javascript. You can easily write your own loaders running in node.js.

## Support

webpack supports **AMD and CommonJs** module styles. It perform clever static analysis on the AST of your code. It even has a evaluation engine to evaluate simple expressions. This allows you to **support most existing libraries**.

## Code Splitting

webpack allows to split your codebase into chunks. Chunks are loaded **on demand**. This reduces initial loading time.

## Optimizations

webpack can do many optimizations to **reduce the output size**. It also cares about **caching** by using hashes.



# A small example what's possible

``` javascript
var commonjs = require("./commonjs");
define(["amd-module", "./file"], function(amdModule, file) {
	require(["big-module/big/file"], function(big) {
		// AMD require acts as split point
		// and "big-module/big/file" is only downloaded when requested
		var stuff = require("../my/stuff");
		// dependencies automatically goes in chunk too
	});
});

require("coffee!./cup.coffee");
// The loader syntax allows to proprocess files
// for common stuff you can bind RegExps to loaders
// if you also add ".coffee" to the default extensions
// you can write:
require("./cup");

function loadTemplate(name) {
	return require("./templates/" + name ".jade");
	// dynamic requires are supported
	// while compiling we figure out what can be requested
	// here everything in "./templates" that matches /^.*\.jade$/
	// (can also be in subdirectories)
}

require("imports?_=underscore!../loaders/my-ejs-loader!./template.html");
// you can chain loaders
// you can configure loaders with query parameters
// and loaders resolve similar to modules

// ...you can combine everything
function loadTemplateAsync(name, callback) {
	require(["bundle?lazy!./templates/" + name + ".jade"], function(templateBundle) {
		templateBundle(callback);
	});
}
```



## Documentation

[documentation](http://webpack.github.io/docs/?utm_source=github&utm_medium=readme&utm_campaign=documentation)



## Tests

You can run the node tests with `npm test`. [![build status](https://secure.travis-ci.org/webpack/webpack.png)](http://travis-ci.org/webpack/webpack)

You can run the browser tests:

```
cd test/browsertests
node build
```

and open `tests.html` in browser.



## Contribution

You are welcome to contribute by writing issues or pull requests.
It would be nice if you open source your own loaders or webmodules. :)

You are also welcome to correct any spelling mistakes or any language issues, because my english is not perfect...

If you want to discus something or just need help, [here is a gitter.im room](https://gitter.im/webpack/webpack).


## License

Copyright (c) 2012-2014 Tobias Koppers

MIT (http://www.opensource.org/licenses/mit-license.php)




## Dependencies

* [esprima](http://esprima.org/)
* [enhanced-resolve](https://github.com/webpack/enhanced-resolve)
* [uglify-js](https://github.com/mishoo/UglifyJS)
* [mocha](https://github.com/visionmedia/mocha)
* [should](https://github.com/visionmedia/should.js)
* [optimist](https://github.com/substack/node-optimist)
* [async](https://github.com/caolan/async)
* [mkdirp](http://esprima.org/)
* [clone](https://github.com/pvorb/node-clone)
* [base64-encode](https://github.com/ForbesLindesay/base64-encode)

[![Dependency Status](https://david-dm.org/webpack/webpack.png)](https://david-dm.org/webpack/webpack)
