# api documentation for  [x-ray (v2.3.2)](https://github.com/lapwinglabs/x-ray#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-x-ray.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-x-ray) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-x-ray.svg)](https://travis-ci.org/npmdoc/node-npmdoc-x-ray)
#### structure any website

[![NPM](https://nodei.co/npm/x-ray.png?downloads=true)](https://www.npmjs.com/package/x-ray)

[![apidoc](https://npmdoc.github.io/node-npmdoc-x-ray/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-x-ray_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-x-ray/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-x-ray/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "Matthew Mueller",
        "email": "matt@lapwinglabs.com"
    },
    "bugs": {
        "url": "https://github.com/lapwinglabs/x-ray/issues"
    },
    "contributors": [
        {
            "name": "Fabien Franzen",
            "email": "info@atelierfabien.be"
        }
    ],
    "dependencies": {
        "batch": "~0.5.2",
        "chalk": "~1.1.1",
        "cheerio": "~0.20.0",
        "debug": "~2.2.0",
        "enstore": "~1.0.1",
        "is-url": "~1.2.0",
        "isobject": "~2.0.0",
        "object-assign": "~4.0.1",
        "x-ray-crawler": "~2.0.1",
        "x-ray-parse": "~1.0.1"
    },
    "description": "structure any website",
    "devDependencies": {
        "concat-stream": "~1.5.1",
        "coveralls": "~2.11.8",
        "istanbul": "~0.4.2",
        "mocha": "latest",
        "mocha-lcov-reporter": "~1.2.0",
        "multiline": "~1.0.2",
        "rimraf": "~2.5.2",
        "standard": "~6.0.8"
    },
    "directories": {},
    "dist": {
        "shasum": "5d1ecc84b48a01ebea73f70a6fa0d1171bbc39e4",
        "tarball": "https://registry.npmjs.org/x-ray/-/x-ray-2.3.2.tgz"
    },
    "engines": {
        "node": ">= 0.10"
    },
    "gitHead": "d9996bc9166905c3a44256c976ec9184800f1c45",
    "homepage": "https://github.com/lapwinglabs/x-ray#readme",
    "keywords": [
        "api",
        "cheerio",
        "scrape",
        "scraper",
        "structure",
        "web"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "kikobeats",
            "email": "josefrancisco.verdu@gmail.com"
        },
        {
            "name": "mattmueller",
            "email": "mattmuelle@gmail.com"
        }
    ],
    "name": "x-ray",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/lapwinglabs/x-ray.git"
    },
    "scripts": {
        "coveralls": "istanbul cover ./node_modules/.bin/_mocha --report lcovonly",
        "pretest": "standard",
        "test": "mocha"
    },
    "version": "2.3.2"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module x-ray](#apidoc.module.x-ray)
1.  object <span class="apidocSignatureSpan">x-ray.</span>stream
1.  object <span class="apidocSignatureSpan">x-ray.</span>util

#### [module x-ray.stream](#apidoc.module.x-ray.stream)
1.  [function <span class="apidocSignatureSpan">x-ray.stream.</span>array (stream)](#apidoc.element.x-ray.stream.array)
1.  [function <span class="apidocSignatureSpan">x-ray.stream.</span>object (stream)](#apidoc.element.x-ray.stream.object)
1.  [function <span class="apidocSignatureSpan">x-ray.stream.</span>waitCb (stream, fn)](#apidoc.element.x-ray.stream.waitCb)

#### [module x-ray.util](#apidoc.module.x-ray.util)
1.  [function <span class="apidocSignatureSpan">x-ray.util.</span>compact (arr)](#apidoc.element.x-ray.util.compact)
1.  [function <span class="apidocSignatureSpan">x-ray.util.</span>isArray ()](#apidoc.element.x-ray.util.isArray)
1.  [function <span class="apidocSignatureSpan">x-ray.util.</span>isHTML (str)](#apidoc.element.x-ray.util.isHTML)
1.  [function <span class="apidocSignatureSpan">x-ray.util.</span>isObject (o)](#apidoc.element.x-ray.util.isObject)
1.  [function <span class="apidocSignatureSpan">x-ray.util.</span>isUrl (string)](#apidoc.element.x-ray.util.isUrl)
1.  [function <span class="apidocSignatureSpan">x-ray.util.</span>objectAssign ()](#apidoc.element.x-ray.util.objectAssign)
1.  [function <span class="apidocSignatureSpan">x-ray.util.</span>root (selector)](#apidoc.element.x-ray.util.root)



# <a name="apidoc.module.x-ray"></a>[module x-ray](#apidoc.module.x-ray)



# <a name="apidoc.module.x-ray.stream"></a>[module x-ray.stream](#apidoc.module.x-ray.stream)

#### <a name="apidoc.element.x-ray.stream.array"></a>[function <span class="apidocSignatureSpan">x-ray.stream.</span>array (stream)](#apidoc.element.x-ray.stream.array)
- description and source-code
```javascript
function stream_array(stream) {
  if (!stream) return function () {}
  var first = true

  return function _stream_array (data, end) {
    var json = JSON.stringify(data, true, 2)

    if (first) {
      stream.write('[\n')
      first = false
    }

    if (isArray(data)) {
      json = json.slice(1, -1)
    }

    if (end) {
      stream.end(json + ']')
    } else {
      stream.write(json + ',')
    }
  }
}
```
- example usage
```shell
...
      function next (err, obj, $) {
if (err) return fn(err)
var paginate = state.paginate
var limit = --state.limit

// create the stream
if (!stream) {
  if (paginate) stream = streamHelper.array(state.stream)
  else stream = streamHelper.object(state.stream)
}

if (paginate) {
  if (isArray(obj)) {
    pages = pages.concat(obj)
  } else {
...
```

#### <a name="apidoc.element.x-ray.stream.object"></a>[function <span class="apidocSignatureSpan">x-ray.stream.</span>object (stream)](#apidoc.element.x-ray.stream.object)
- description and source-code
```javascript
function stream_object(stream) {
  if (!stream) return function () {}

  return function _stream_object (data, end) {
    var json = JSON.stringify(data, true, 2)

    if (end) {
      stream.end(json)
    } else {
      stream.write(json)
    }
  }
}
```
- example usage
```shell
...
if (err) return fn(err)
var paginate = state.paginate
var limit = --state.limit

// create the stream
if (!stream) {
  if (paginate) stream = streamHelper.array(state.stream)
  else stream = streamHelper.object(state.stream)
}

if (paginate) {
  if (isArray(obj)) {
    pages = pages.concat(obj)
  } else {
    pages.push(obj)
...
```

#### <a name="apidoc.element.x-ray.stream.waitCb"></a>[function <span class="apidocSignatureSpan">x-ray.stream.</span>waitCb (stream, fn)](#apidoc.element.x-ray.stream.waitCb)
- description and source-code
```javascript
function stream_callback(stream, fn) {
  fn(function (err) {
    if (err) stream.emit('error', err)
  })
}
```
- example usage
```shell
...
  state.limit = limit
  return node
}

node.stream = function () {
  state.stream = store.createWriteStream()
  var rs = store.createReadStream()
  streamHelper.waitCb(rs, node)
  return rs
}

node.write = function (path) {
  if (!arguments.length) return node.stream()
  state.stream = fs.createWriteStream(path)
  streamHelper.waitCb(state.stream, node)
...
```



# <a name="apidoc.module.x-ray.util"></a>[module x-ray.util](#apidoc.module.x-ray.util)

#### <a name="apidoc.element.x-ray.util.compact"></a>[function <span class="apidocSignatureSpan">x-ray.util.</span>compact (arr)](#apidoc.element.x-ray.util.compact)
- description and source-code
```javascript
function compact(arr) {
  return arr.filter(function (val) {
    if (!val) return false
    if (val.length !== undefined) return val.length !== 0
    for (var key in val) if (has.call(val, key)) return true
    return false
  })
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.x-ray.util.isArray"></a>[function <span class="apidocSignatureSpan">x-ray.util.</span>isArray ()](#apidoc.element.x-ray.util.isArray)
- description and source-code
```javascript
function isArray() { [native code] }
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.x-ray.util.isHTML"></a>[function <span class="apidocSignatureSpan">x-ray.util.</span>isHTML (str)](#apidoc.element.x-ray.util.isHTML)
- description and source-code
```javascript
function isHTML(str) {
  str = (str || '').toString().trim()
  return str[0] === '<' && str[str.length - 1] === '>'
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.x-ray.util.isObject"></a>[function <span class="apidocSignatureSpan">x-ray.util.</span>isObject (o)](#apidoc.element.x-ray.util.isObject)
- description and source-code
```javascript
function isObject(o) {
  return o != null && typeof o === 'object' && !isArray(o);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.x-ray.util.isUrl"></a>[function <span class="apidocSignatureSpan">x-ray.util.</span>isUrl (string)](#apidoc.element.x-ray.util.isUrl)
- description and source-code
```javascript
function isUrl(string){
  return matcher.test(string);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.x-ray.util.objectAssign"></a>[function <span class="apidocSignatureSpan">x-ray.util.</span>objectAssign ()](#apidoc.element.x-ray.util.objectAssign)
- description and source-code
```javascript
function assign() { [native code] }
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.x-ray.util.root"></a>[function <span class="apidocSignatureSpan">x-ray.util.</span>root (selector)](#apidoc.element.x-ray.util.root)
- description and source-code
```javascript
function root(selector) {
  return (typeof selector === 'string' || isArray(selector)) &&
  !~selector.indexOf('@') &&
  !isUrl(selector) &&
  selector
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
