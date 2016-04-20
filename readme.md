mithril-objectify [![NPM Version](https://img.shields.io/npm/v/mithril-objectify.svg)](https://www.npmjs.com/package/mithril-objectify) [![NPM License](https://img.shields.io/npm/l/mithril-objectify.svg)](https://www.npmjs.com/package/mithril-objectify)
=================

<p align="center">
    <a href="https://www.npmjs.com/package/mithril-objectify" alt="NPM Downloads">
        <img src="https://img.shields.io/npm/dm/mithril-objectify.svg" />
    </a>
    <a href="https://travis-ci.org/tivac/mithril-objectify" alt="Build Status">
        <img src="https://img.shields.io/travis/tivac/mithril-objectify/master.svg" />
    </a>
    <a href="https://david-dm.org/tivac/mithril-objectify" alt="Dependency Status">
        <img src="https://img.shields.io/david/tivac/mithril-objectify.svg" />
    </a>
    <a href="https://david-dm.org/tivac/mithril-objectify#info=devDependencies" alt="devDependency Status">
        <img src="https://img.shields.io/david/dev/tivac/mithril-objectify.svg" />
    </a>
</p>


Turn [mithril](http://mithril.js.org) html functions like `m(".fooga")` into static JS objects like:

```js
{ tag: "div", attrs: { "className" : "fooga" }, children: [ ] }
```

for speeeeeed.

Use via [CLI](#cli), [JS API](#js-api), [Browserify](#browserify), or [Rollup](#rollup)!

Please file an issue if you come across any cases that this doesn't handle, I'd love to improve the number of structures I can rewrite!

## Installation

Install with npm

`npm i mithril-objectify`

## Usage

### CLI

Accepts an input file and optional output file. No output file will echo the result to stdout.

```
> mithril-objectify ./input.js
> mithril-objectify ./input.js ./output.js
```

### JS API

Accepts a string or buffer, returns a buffer.

```js
var objectify = require("mithril-objectify");

console.log(objectify(`m(".fooga.wooga.booga")`);

// logs
// ({ tag: "div", attrs: { className: "fooga wooga booga" }, children: [ ] })
```

### Browserify

Use as a browserify transform, either via the CLI or via code.

#### CLI
Using `mithril-objectify` with browserify on the CLI.

`browserify -t mithril-objectify/browserify <file>`

#### API
Or you can add the transform using the JS API.

```js
var build = require("browserify")();

build.transform("mithril-objectify/browserify");

b.add("./client.js");

b.bundle().pipe(process.stdout);
```

### Rollup

Use as a rollup plugin.

```js
rollup.rollup({
    entry   : "./entry.js",
    plugins : [
        require("mithril-objectify/rollup")()
    ]
})
.then(function(bundle) {
    return bundle.write({
        dest : "./out/source.js"
    });
})
```
