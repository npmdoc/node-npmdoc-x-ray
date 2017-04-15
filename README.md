# api documentation for  [x-ray (v2.3.2)](https://github.com/lapwinglabs/x-ray#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-x-ray.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-x-ray) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-x-ray.svg)](https://travis-ci.org/npmdoc/node-npmdoc-x-ray)
#### structure any website

[![NPM](https://nodei.co/npm/x-ray.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/x-ray)

[![apidoc](https://npmdoc.github.io/node-npmdoc-x-ray/build/screenCapture.buildCi.browser.apidoc.html.png)](https://npmdoc.github.io/node-npmdoc-x-ray/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-x-ray/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-x-ray/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Matthew Mueller"
    },
    "bugs": {
        "url": "https://github.com/lapwinglabs/x-ray/issues"
    },
    "contributors": [
        {
            "name": "Fabien Franzen"
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
            "name": "kikobeats"
        },
        {
            "name": "mattmueller"
        }
    ],
    "name": "x-ray",
    "optionalDependencies": {},
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
1.  [function <span class="apidocSignatureSpan"></span>x-ray (options)](#apidoc.element.x-ray.x-ray)
1.  [function <span class="apidocSignatureSpan">x-ray.</span>toString ()](#apidoc.element.x-ray.toString)



# <a name="apidoc.module.x-ray"></a>[module x-ray](#apidoc.module.x-ray)

#### <a name="apidoc.element.x-ray.x-ray"></a>[function <span class="apidocSignatureSpan"></span>x-ray (options)](#apidoc.element.x-ray.x-ray)
- description and source-code
```javascript
function Xray(options) {
  var crawler = Crawler()
  options = options || {}
  var filters = options.filters || {}

  function xray (source, scope, selector) {
    var args = params(source, scope, selector)
    selector = args.selector
    source = args.source
    scope = args.context

    var state = objectAssign({}, CONST.INIT_STATE)
    var store = enstore()
    var pages = []
    var stream

    var walkHTML = WalkHTML(xray, selector, scope, filters)
    var request = Request(crawler)

    function node (source2, fn) {
      if (arguments.length === 1) {
        fn = source2
      } else {
        source = source2
      }

      debug('params: %j', {
        source: source,
        scope: scope,
        selector: selector
      })

      if (isUrl(source)) {
        debug('starting at: %s', source)
        request(source, function (err, html) {
          if (err) return next(err)
          var $ = load(html, source)
          walkHTML($, next)
        })
      } else if (scope && ~scope.indexOf('@')) {
        debug('resolving to a url: %s', scope)
        var url = resolve(source, false, scope, filters)

        // ensure that a@href is a URL
        if (!isUrl(url)) {
          debug('%s is not a url. Skipping!', url)
          return walkHTML(load(''), next)
        }

        debug('resolved "%s" to a %s', scope, url)
        request(url, function (err, html) {
          if (err) return next(err)
          var $ = load(html, url)
          walkHTML($, next)
        })
      } else if (source) {
        var $ = load(source)
        walkHTML($, next)
      } else {
        debug('%s is not a url or html. Skipping!', source)
        return walkHTML(load(''), next)
      }

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
            pages.push(obj)
          }

          if (limit <= 0) {
            debug('reached limit, ending')
            stream(obj, true)
            return fn(null, pages)
          }

          var url = resolve($, false, paginate, filters)
          debug('paginate(%j) => %j', paginate, url)

          if (!isUrl(url)) {
            debug('%j is not a url, finishing up', url)
            stream(obj, true)
            return fn(null, pages)
          }

          stream(obj)

          // debug
          debug('paginating %j', url)
          isFinite(limit) && debug('%s page(s) left to crawl', limit)

          request(url, function (err, html) {
            if (err) return next(err)
            var $ = load(html, url)
            walkHTML($, next)
          })
        } else {
          stream(obj, true)
          fn(null, obj)
        }
      }

      return node
    }

    node.paginate = function (paginate) {
      if (!arguments.length) return state.paginate
      state.paginate = paginate
      return node
    }

    node.limit = function (limit) {
      if (!arguments.length) return state.limit
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
      return state.stream
    }

    return node
  }

  CONST.CRAWLER_METHODS.forEach(function (method) {
    xray[method] = function () {
      if (!arguments.length) return crawler[method]()
      crawler[method].apply(crawler, arguments)
      return this
    }
  })

  return xray
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.x-ray.toString"></a>[function <span class="apidocSignatureSpan">x-ray.</span>toString ()](#apidoc.element.x-ray.toString)
- description and source-code
```javascript
toString = function () {
    return toString;
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
