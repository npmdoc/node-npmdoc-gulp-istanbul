# api documentation for  [gulp-istanbul (v1.1.1)](https://github.com/SBoudrias/gulp-istanbul)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-istanbul.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-istanbul) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-istanbul.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-istanbul)
#### Istanbul unit test coverage plugin for gulp.

[![NPM](https://nodei.co/npm/gulp-istanbul.png?downloads=true)](https://www.npmjs.com/package/gulp-istanbul)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-istanbul/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gulp-istanbul_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-istanbul/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-istanbul/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-istanbul/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Simon Boudrias",
        "email": "admin@simonboudrias.com",
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
            "name": "sboudrias",
            "email": "admin@simonboudrias.com"
        }
    ],
    "name": "gulp-istanbul",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
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



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-istanbul](#apidoc.module.gulp-istanbul)
1.  [function <span class="apidocSignatureSpan">gulp-istanbul.</span>enforceThresholds (opts)](#apidoc.element.gulp-istanbul.enforceThresholds)
1.  [function <span class="apidocSignatureSpan">gulp-istanbul.</span>hookRequire (options)](#apidoc.element.gulp-istanbul.hookRequire)
1.  [function <span class="apidocSignatureSpan">gulp-istanbul.</span>summarizeCoverage (opts)](#apidoc.element.gulp-istanbul.summarizeCoverage)
1.  [function <span class="apidocSignatureSpan">gulp-istanbul.</span>writeReports (opts)](#apidoc.element.gulp-istanbul.writeReports)



# <a name="apidoc.module.gulp-istanbul"></a>[module gulp-istanbul](#apidoc.module.gulp-istanbul)

#### <a name="apidoc.element.gulp-istanbul.enforceThresholds"></a>[function <span class="apidocSignatureSpan">gulp-istanbul.</span>enforceThresholds (opts)](#apidoc.element.gulp-istanbul.enforceThresholds)
- description and source-code
```javascript
enforceThresholds = function (opts) {
  opts = opts || {};
  opts = _.defaults(opts, {
    coverageVariable: COVERAGE_VARIABLE
  });

  var cover = through();

  cover.on('end', function () {
    var collector = new Collector();

    // Revert to an object if there are no macthing source files.
    collector.add(global[opts.coverageVariable] || {});

    var results = checker.checkFailures(opts.thresholds, collector.getFinalCoverage());
    var criteria = function(type) {
      return (type.global && type.global.failed) || (type.each && type.each.failed);
    };

    if (_.some(results, criteria)) {
      this.emit('error', new PluginError({
        plugin: PLUGIN_NAME,
        message: 'Coverage failed'
      }));
    }

  }).resume();

  return cover;
}
```
- example usage
```shell
...

gulp.task('test', ['pre-test'], function () {
  return gulp.src(['test/*.js'])
    .pipe(mocha())
    // Creating the reports after tests ran
    .pipe(istanbul.writeReports())
    // Enforce a coverage of at least 90%
    .pipe(istanbul.enforceThresholds({ thresholds: { global: 90 } }));
});
'''

#### Browser testing

For browser testing, you'll need to write the files covered by istanbul in a directory from where you'll serve these files to the
 browser running the test. You'll also need a way to extract the value of the [coverage variable](#coveragevariable) after the test
 have runned in the browser.
...
```

#### <a name="apidoc.element.gulp-istanbul.hookRequire"></a>[function <span class="apidocSignatureSpan">gulp-istanbul.</span>hookRequire (options)](#apidoc.element.gulp-istanbul.hookRequire)
- description and source-code
```javascript
hookRequire = function (options) {
  var fileMap = {};

  istanbul.hook.unhookRequire();
  istanbul.hook.hookRequire(function (path) {
    return !!fileMap[normalizePathSep(path)];
  }, function (code, path) {
    return fileMap[normalizePathSep(path)];
  }, options);

  return through(function (file, enc, cb) {
    // If the file is already required, delete it from the cache otherwise the covered
    // version will be ignored.
    delete require.cache[path.resolve(file.path)];
    fileMap[normalizePathSep(file.path)] = file.contents.toString();
    return cb();
  });
}
```
- example usage
```shell
...
var mocha = require('gulp-mocha');

gulp.task('pre-test', function () {
return gulp.src(['lib/**/*.js'])
  // Covering files
  .pipe(istanbul())
  // Force 'require' to return covered files
  .pipe(istanbul.hookRequire());
});

gulp.task('test', ['pre-test'], function () {
return gulp.src(['test/*.js'])
  .pipe(mocha())
  // Creating the reports after tests ran
  .pipe(istanbul.writeReports())
...
```

#### <a name="apidoc.element.gulp-istanbul.summarizeCoverage"></a>[function <span class="apidocSignatureSpan">gulp-istanbul.</span>summarizeCoverage (opts)](#apidoc.element.gulp-istanbul.summarizeCoverage)
- description and source-code
```javascript
summarizeCoverage = function (opts) {
  opts = opts || {};
  if (!opts.coverageVariable) opts.coverageVariable = COVERAGE_VARIABLE;

  if (!global[opts.coverageVariable]) throw new Error('no coverage data found, run tests before calling 'summarizeCoverage'');

  var collector = new Collector();
  collector.add(global[opts.coverageVariable]);
  return istanbul.utils.summarizeCoverage(collector.getFinalCoverage());
}
```
- example usage
```shell
...

### istanbul.hookRequire()

Overwrite 'require' so it returns the covered files. The method take an optional [option object](https://gotwarlost.github.io/istanbul
/public/apidocs/classes/Hook.html#method_hookRequire).

Always use this option if you're running tests in Node.js

### istanbul.summarizeCoverage(opt)

get coverage summary details

#### opt
Type: 'Object' (optional)
'''js
{
...
```

#### <a name="apidoc.element.gulp-istanbul.writeReports"></a>[function <span class="apidocSignatureSpan">gulp-istanbul.</span>writeReports (opts)](#apidoc.element.gulp-istanbul.writeReports)
- description and source-code
```javascript
writeReports = function (opts) {
  if (typeof opts === 'string') opts = { dir: opts };
  opts = opts || {};

  var defaultDir = path.join(process.cwd(), 'coverage');
  opts = _.defaultsDeep(opts, {
    coverageVariable: COVERAGE_VARIABLE,
    dir: defaultDir,
    reportOpts: {
      dir: opts.dir || defaultDir
    }
  });
  opts.reporters = opts.reporters || [ 'lcov', 'json', 'text', 'text-summary' ];

  var reporters = opts.reporters.map(function(reporter) {
    if (reporter.TYPE) Report.register(reporter);
    return reporter.TYPE || reporter;
  });

  var invalid = _.difference(reporters, Report.getReportList());
  if (invalid.length) {
    // throw before we start -- fail fast
    throw new PluginError(PLUGIN_NAME, 'Invalid reporters: ' + invalid.join(', '));
  }

  reporters = reporters.map(function (r) {
    var reportOpts = opts.reportOpts[r] || opts.reportOpts;
    return Report.create(r, _.clone(reportOpts));
  });

  var cover = through();

  cover.on('end', function () {
    var collector = new Collector();

    // Revert to an object if there are no matching source files.
    collector.add(global[opts.coverageVariable] || {});

    reporters.forEach(function (report) {
      report.writeReport(collector, true);
    });
  }).resume();

  return cover;
}
```
- example usage
```shell
...
    .pipe(istanbul.hookRequire());
});

gulp.task('test', ['pre-test'], function () {
  return gulp.src(['test/*.js'])
    .pipe(mocha())
    // Creating the reports after tests ran
    .pipe(istanbul.writeReports())
    // Enforce a coverage of at least 90%
    .pipe(istanbul.enforceThresholds({ thresholds: { global: 90 } }));
});
'''

#### Browser testing
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
