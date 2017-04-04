# api documentation for  [through2-map (v3.0.0)](https://github.com/brycebaril/through2-map#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-through2-map.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-through2-map) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-through2-map.svg)](https://travis-ci.org/npmdoc/node-npmdoc-through2-map)
#### A through2 to create an Array.prototype.map analog for streams.

[![NPM](https://nodei.co/npm/through2-map.png?downloads=true)](https://www.npmjs.com/package/through2-map)

[![apidoc](https://npmdoc.github.io/node-npmdoc-through2-map/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-through2-map_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-through2-map/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-through2-map/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-through2-map/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Bryce B. Baril"
    },
    "bugs": {
        "url": "https://github.com/brycebaril/through2-map/issues"
    },
    "dependencies": {
        "through2": "~2.0.0",
        "xtend": "^4.0.0"
    },
    "description": "A through2 to create an Array.prototype.map analog for streams.",
    "devDependencies": {
        "stream-spigot": "~3.0.5",
        "tape": "~4.0.0",
        "terminus": "~1.0.12"
    },
    "directories": {
        "test": "test"
    },
    "dist": {
        "shasum": "a6c3026ce63b4898a997d540506b66ffd970f271",
        "tarball": "https://registry.npmjs.org/through2-map/-/through2-map-3.0.0.tgz"
    },
    "gitHead": "8a482d218bdf2de40bf867a1f28ffa9fa0a3b315",
    "homepage": "https://github.com/brycebaril/through2-map#readme",
    "jshintConfig": {
        "asi": true,
        "globalstrict": true,
        "validthis": true,
        "eqnull": true,
        "node": true,
        "loopfunc": true,
        "newcap": false,
        "eqeqeq": false
    },
    "keywords": [
        "streams",
        "through",
        "through2",
        "map"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "bryce",
            "email": "bryce@ravenwall.com"
        }
    ],
    "name": "through2-map",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+ssh://git@github.com/brycebaril/through2-map.git"
    },
    "scripts": {
        "test": "node test/"
    },
    "version": "3.0.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module through2-map](#apidoc.module.through2-map)
1.  [function <span class="apidocSignatureSpan">through2-map.</span>ctor (options, fn)](#apidoc.element.through2-map.ctor)
1.  [function <span class="apidocSignatureSpan">through2-map.</span>obj (options, fn)](#apidoc.element.through2-map.obj)
1.  [function <span class="apidocSignatureSpan">through2-map.</span>objCtor (options, fn)](#apidoc.element.through2-map.objCtor)



# <a name="apidoc.module.through2-map"></a>[module through2-map](#apidoc.module.through2-map)

#### <a name="apidoc.element.through2-map.ctor"></a>[function <span class="apidocSignatureSpan">through2-map.</span>ctor (options, fn)](#apidoc.element.through2-map.ctor)
- description and source-code
```javascript
function ctor(options, fn) {
  if (typeof options == "function") {
    fn = options
    options = {}
  }

  var Map = through2.ctor(options, function (chunk, encoding, callback) {
    if (this.options.wantStrings) chunk = chunk.toString()
    try {
      this.push(fn.call(this, chunk, this._index++))
      return callback()
    } catch (e) {
      return callback(e)
    }
  })
  Map.prototype._index = 0
  return Map
}
```
- example usage
```shell
...
'''

Create a 'stream.Transform' instance that will call 'fn(chunk, index)' on each stream segment.

- - -

'''
var Tx = require("through2-map").ctor([options,] fn)
'''

Create a reusable 'stream.Transform' TYPE that can be called via 'new Tx' or 'Tx()' to create an instance.

- - -

'''
...
```

#### <a name="apidoc.element.through2-map.obj"></a>[function <span class="apidocSignatureSpan">through2-map.</span>obj (options, fn)](#apidoc.element.through2-map.obj)
- description and source-code
```javascript
function obj(options, fn) {
  if (typeof options === "function") {
    fn = options
    options = {}
  }
  options = xtend({objectMode: true, highWaterMark: 16}, options)
  return make(options, fn)
}
```
- example usage
```shell
...
'''

Create a reusable 'stream.Transform' TYPE that can be called via 'new Tx' or 'Tx()' to create an instance.

- - -

'''
require("through2-map").obj([options,] fn)
'''

Create a 'through2-map' instance that defaults to 'objectMode: true'.

- - -

'''
...
```

#### <a name="apidoc.element.through2-map.objCtor"></a>[function <span class="apidocSignatureSpan">through2-map.</span>objCtor (options, fn)](#apidoc.element.through2-map.objCtor)
- description and source-code
```javascript
function objCtor(options, fn) {
  if (typeof options === "function") {
    fn = options
    options = {}
  }
  options = xtend({objectMode: true, highWaterMark: 16}, options)
  return ctor(options, fn)
}
```
- example usage
```shell
...
'''

Create a 'through2-map' instance that defaults to 'objectMode: true'.

- - -

'''
require("through2-map").objCtor([options,] fn)
'''

Just like ctor, but with 'objectMode: true' defaulting to true.

Options
-------
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
