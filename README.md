# npmdoc-x-ray

#### api documentation for  [x-ray (v2.3.2)](https://github.com/lapwinglabs/x-ray#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-x-ray.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-x-ray) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-x-ray.svg)](https://travis-ci.org/npmdoc/node-npmdoc-x-ray)

#### structure any website

[![NPM](https://nodei.co/npm/x-ray.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/x-ray)

- [https://npmdoc.github.io/node-npmdoc-x-ray/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-x-ray/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-x-ray/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-x-ray/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-x-ray/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-x-ray/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "name": "x-ray",
    "description": "structure any website",
    "homepage": "https://github.com/lapwinglabs/x-ray#readme",
    "version": "2.3.2",
    "main": "index.js",
    "author": {
        "name": "Matthew Mueller"
    },
    "contributors": [
        {
            "name": "Fabien Franzen"
        }
    ],
    "repository": {
        "type": "git",
        "url": "git://github.com/lapwinglabs/x-ray.git"
    },
    "bugs": {
        "url": "https://github.com/lapwinglabs/x-ray/issues"
    },
    "keywords": [
        "api",
        "cheerio",
        "scrape",
        "scraper",
        "structure",
        "web"
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
    "engines": {
        "node": ">= 0.10"
    },
    "scripts": {
        "coveralls": "./node_modules/.bin/istanbul cover ./node_modules/.bin/_mocha --report lcovonly",
        "pretest": "standard",
        "test": "mocha"
    },
    "license": "MIT"
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
