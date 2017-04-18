# npmdoc-gulp-istanbul

#### api documentation for  [gulp-istanbul (v1.1.1)](https://github.com/SBoudrias/gulp-istanbul)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-istanbul.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-istanbul) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-istanbul.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-istanbul)

#### Istanbul unit test coverage plugin for gulp.

[![NPM](https://nodei.co/npm/gulp-istanbul.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/gulp-istanbul)

- [https://npmdoc.github.io/node-npmdoc-gulp-istanbul/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-gulp-istanbul/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-istanbul/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-istanbul/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-istanbul/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-istanbul/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Simon Boudrias",
        "url": "https://github.com/SBoudrias"
    },
    "bugs": {
        "url": "https://github.com/SBoudrias/gulp-istanbul/issues"
    },
    "dependencies": {
        "gulp-util": "^3.0.1",
        "istanbul": "^0.4.0",
        "istanbul-threshold-checker": "^0.1.0",
        "lodash": "^4.0.0",
        "through2": "^2.0.0",
        "vinyl-sourcemaps-apply": "^0.2.1"
    },
    "description": "Istanbul unit test coverage plugin for gulp.",
    "devDependencies": {
        "gulp": "^3.6.2",
        "gulp-mocha": "^3.0.1",
        "gulp-sourcemaps": "^1.6.0",
        "isparta": "^4.0.0",
        "jshint": "^2.5.0",
        "mocha": "^3.0.2",
        "rimraf": "^2.2.8"
    },
    "directories": {},
    "dist": {
        "shasum": "e094d98f42bfa4d9a8e5366f414ed9a09a3c6537",
        "tarball": "https://registry.npmjs.org/gulp-istanbul/-/gulp-istanbul-1.1.1.tgz"
    },
    "files": [
        "index.js"
    ],
    "gitHead": "a8dd45ebbf9692fefbe7aa5081b6aeda74eb4ac1",
    "homepage": "https://github.com/SBoudrias/gulp-istanbul",
    "keywords": [
        "gulpplugin",
        "coverage",
        "istanbul",
        "unit test"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "sboudrias"
        }
    ],
    "name": "gulp-istanbul",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git://github.com/SBoudrias/gulp-istanbul.git"
    },
    "scripts": {
        "pretest": "jshint index.js ./test/.",
        "test": "mocha -R spec"
    },
    "version": "1.1.1"
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
