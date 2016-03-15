ZKflow for AngularJS
====================

Gulp tasks for AngularJS projects powered by [ZKflow](https://github.com/zaklinaczekodu/zkflow)

[<img alt="Made by Zaklinacze Kodu" src="http://zaklinaczekodu.com/_assets/madeBy.svg" width="200">](http://zaklinaczekodu.com)

Shields
-------

[![npm](https://img.shields.io/npm/v/zkflow-angular.svg?style=flat-square)](https://www.npmjs.com/package/zkflow-angular)
[![npm](https://img.shields.io/npm/l/zkflow-angular.svg?style=flat-square)](https://www.npmjs.com/package/zkflow-angular)
[![npm](https://img.shields.io/npm/dm/zkflow-angular.svg?style=flat-square)](https://www.npmjs.com/package/zkflow-angular)<br>
[![Travis](https://img.shields.io/travis/zaklinaczekodu/zkflow-angular/master.svg?style=flat-square)](https://travis-ci.org/zaklinaczekodu/zkflow-angular)
[![Code Climate](https://img.shields.io/codeclimate/github/zaklinaczekodu/zkflow-angular.svg?style=flat-square)](https://codeclimate.com/github/zaklinaczekodu/zkflow-angular)<br>
[![David](https://img.shields.io/david/zaklinaczekodu/zkflow-angular.svg?style=flat-square)](https://david-dm.org/zaklinaczekodu/zkflow-angular)
[![David](https://img.shields.io/david/dev/zaklinaczekodu/zkflow-angular.svg?style=flat-square)](https://david-dm.org/zaklinaczekodu/zkflow-angular)<br>
[![GitHub forks](https://img.shields.io/github/forks/zaklinaczekodu/zkflow-angular.svg?style=flat-square)](https://github.com/zaklinaczekodu/zkflow-angular)
[![GitHub stars](https://img.shields.io/github/stars/zaklinaczekodu/zkflow-angular.svg?style=flat-square)](https://github.com/zaklinaczekodu/zkflow-angular)
[![GitHub followers](https://img.shields.io/github/followers/zaklinaczekodu.svg?style=flat-square)](https://github.com/zaklinaczekodu/zkflow-angular)

Features
--------

* Sass + sassdoc + css globbing + autoprefixer
* Browserify + ngannotate
* Assets management
* AngularJS templates embedded in js
* E2E tests with protractor and cucumber
* Development environment
    * Webserver with livereload
    * Watching files for changes and full, fast, incremental rebuilds
    * Unit tests with karma
    * Eslint

* Production environment
    * js, css, jpg, png and svg minification
    * cache busting

* Continous integration
    * build + eslint + tests + e2e with guaranteed non-zero exit status on error

Why not just write tasks yourself?
----------------------------------

Usually simple gulp tasks have a lot of problems, which are resolved in ZKflow

* tasks immune to errors resulting crashed watchers
* tasks parametrized with tasks modes
* tasks cannot run few times simultaneously after few quick changes
* in develop mode if task detect some errors it will hold execution until all errors will be corrected and then it will let the rest of dependent tasks run
* tasks in prod mode always returns non-zero exit status on error

Requirements
------------

You need:

* [nodejs](http://nodejs.org/download/)
* updated npm
* satisfy [node-gyp](https://github.com/TooTallNate/node-gyp) dependencies


### nodejs

If you've never used Node or npm before, you'll need to install Node.
If you use homebrew, do:

```Shell
brew install node
```

Otherwise, you can [download](http://nodejs.org/download/) and install it manually.

### updated npm

Update npm by running

```Shell
npm update npm -g
```

### node-gyp dependencies

Node-gyp is used to compile native extensions to node. Zkflow does not require node-gyp directly, but it is installed
by its dependencies. To install this dependencies properly you need to satisfy node-gyp requirements.
Go to [node-gyp github page](https://github.com/TooTallNate/node-gyp) and follow instructions in "You will also need to install" paragraph in README file (python etc.)

Installation
------------

ZKflow for AngularJS is available through npm

```Shell
npm install --save gulp zkflow-angular
```

Put this line in your gulpfile.js

```JavaScript
require('zkflow-angular').init();
```

This will create a set of tasks in gulp, which you will be able to use from console

Development flow
----------------

How you can use ZKflow gulp tasks to work with Your AngularJS project

### write code and test

Run in project root directory

```Shell
./node_modules/.bin/gulp
```

or

```Shell
./node_modules/.bin/gulp default
```

This task will

* clean whole output dir (dev/)
* bundle all your js with browserify and watch file changes with watchify
* bundle all your styles with sass, css globbing and autoprefix
* generate documentation with sassdoc if enabled
* run eslint and rerun on any js file change
* run tests with karma and browserify and watch file changes with watchify
* bundle your angular templates into angular module (.tmp/templates.js) and rebundle on any template file change
* copy your assets and copy any newly created asset since then
* copy Your index.html and inject styles, scripts, angular main module name into it. Redo on index.html change.
* start gulp-webserver with livereload
* open Your default web browser with proper address.

Write some code, enjoy the results

### write e2e tests

Run in project root directory

```Shell
./node_modules/.bin/gulp e2e
```

This task will

* clean whole output dir (test/)
* same as in default task, but will try to start from test module (where you can put Your e2e mocks)
* run protractor and rerun every time you press 'r'

Write some tests

### autofix your code

Run in project root directory

```Shell
./node_modules/.bin/gulp lint-js
```

all your code will be automatically fixed according to eslint rules

### check everything

Run in project root directory

```Shell
./node_modules/.bin/gulp ci
```

This task will fail if

* code isn't eslinted
* any of karma tests will fail
* any of protractor e2e tests will fail
* build fail (sass, browserify)

You definitely should add this task to your CI server. This task can be splitted into stages.
`./node_modules/.bin/gulp ci` is an equivalent for

```Shell
./node_modules/.bin/gulp ci-static-analysis
./node_modules/.bin/gulp ci-test
./node_modules/.bin/gulp ci-build
./node_modules/.bin/gulp ci-e2e
```

### commit :D

```Shell
git commit -m 'awesome code'
```

Production flow
---------------

### installing

```Shell
npm install
```

### building

```Shell
./node_modules/.bin/gulp build
```

This task will

* clean whole output dir (dist/)
* bundle all your js with browserify and minify with uglifyjs
* bundle all your styles with sass, css globbing, autoprefix and minify with csso
* generate documentation with sassdoc if enabled
* bundle your angular templates into angular module (.tmp/templates.js) and minify with htmlminify
* copy your assets and minify all .png/.jpg/.gif/.svg
* copy Your index.html, htmlminify and inject styles, scripts, angular main module name into it.
* Do cache busting

### Apache/Nginx

Point it to `./dist` directory, and configure your server to fallback to index.html if file not found (to work with router html5 mode)

Directory structure
-------------------

* dist/ - build output
* dev/ - dev output
* test/ - e2e output

Files
-----

### .gitignore

You should probably add this entries in .gitignore file

```
npm-debug.log
node_modules/
.tmp/
dist/
dev/
test/
reports/
docs/
```

### src/index.html

```html
<!DOCTYPE html>
<html ng-app="<%= angularMainModuleName %>" lang="en">

<head>
  <meta charset="UTF-8">
  <title></title>
</head>

<body ng-controller="appNameController">

  <!-- inject:js -->
  <!-- endinject -->
</body>

</html>
```

### src/index.js

```JavaScript
'use strict';

var angular = require('angular');

angular.module('app', [
    require('../.tmp/templates.js').name
  ])
  .controller('appNameController', /** @ngInject */ function() {
  });
```


API
---

If you get 'task not found' error from gulp, you probably should pass gulp to init

```JavaScript
require('zkflow-angular').init(undefined, undefined, require('gulp'));
```

### options


You can pass options object to init function

```JavaScript
require('zkflow-angular').init(options, outputDirsMap);
```

For every task options are merged only 1 level deep. Deeper they will be overwritten.

For example if you have default options
```JavaScript
{
  someTask: {
      option1: 1
      option2: 2
      option3: {
          subOption1: 3
          subOption2: 4
      }
  }
}
```

and you pass to init
```JavaScript
{
  someTask: {
      option1: 11
      option3: {
          subOption1: 5
      }
  }
}
```

actual task options are
```JavaScript
{
  someTask: {
      option1: 11
      option2: 2
      option3: {
          subOption1: 5
      }
  }
}
```

#### Default options

We recommend using as much default options as possible. They are based on our experience with AngularJS and
they set up some solid structure for your project.

```JavaScript
{
  assets: {
    task: require('zkflow-angular/src/tasks/assets'),
    enabled: true,
    dependencies: [],
    globs: 'src/**/_assets/**',
    globsOptions: {
      base: './'
    },
    imagemin: undefined //options for gulp-imagemin
  },
  clean: {
    task: require('zkflow-angular/src/tasks/clean')
    enabled: true,
    dependencies: []
  },
  templates: {
    task: require('zkflow-angular/src/tasks/templates')
    enabled: true,
    dependencies: [],
    globs: [
      'src/**/_templates/*.html',
      'src/**/_templates/**/*.html'
    ],
    globsOptions: undefined,
    minifyHtml: {
      empty: true,
      spare: true,
      quotes: true
    },
    templateCache: {
      standalone: true,
      module: 'zk.templates',
      root: '/',
      moduleSystem: 'browserify',
      templateFooter: '}]).name;'
    },
    templateModuleFileName: 'templates.js',
    outputDir: '.tmp/'
  },
  'webdriver-update': {
    task: require('zkflow-angular/src/tasks/webdriverUpdate')
    enabled: true,
    dependencies: [],
    webdriverUpdate: undefined
  },  
  webserver: {
    task: require('zkflow-angular/src/tasks/webserver')
    enabled: true,
    dependencies: [],
    host: 'localhost',
    docsGlobs: 'docs/',
    docsWebserver: {
      livereload: {
        enable: true,
        port: 35730
      },
      directoryListing: {
        enable: true,
        path: 'docs/'
      },
      open: true,
      port: 8010
    }
  },
  assemble: {
    task: require('zkflow-angular/src/tasks/sequence'),
    enabled: true,
    dependencies: [],
    sequence: [
      'clean', ['inject', 'assets']
    ],
    mode: undefined
  },
  build: {
    task: require('zkflow-angular/src/tasks/sequence'),
    enabled: true,
    dependencies: [],
    sequence: [
      'assemble'
    ],
     mode: {
       env: 'prod',
       watch: false
     }
  },
  ci: {
    task: require('zkflow-angular/src/tasks/sequence'),
    enabled: true,
    dependencies: [],
    sequence: [
      'ci-static-analysis',
      'ci-test',
      'ci-build',
      'ci-e2e'
    ],
    mode: undefined
  },
  'ci-build': {
    task: require('zkflow-angular/src/tasks/sequence'),
    enabled: true,
    dependencies: [],
    sequence: [
      ['assemble']
    ],
    mode: {
      env: 'prod',
      watch: false
    }
  },
  'ci-e2e': {
    task: require('zkflow-angular/src/tasks/sequence'),
    enabled: true,
    dependencies: [],
    sequence: [
      ['e2e']
    ],
    mode: {
      env: 'test',
      watch: false
    }
  },
  'ci-static-analysis': {
    task: require('zkflow-angular/src/tasks/sequence'),
    enabled: true,
    dependencies: [],
    sequence: [
      ['lint-js']
    ],
    mode: {
      env: 'prod',
      watch: false
    }
  },
  'ci-test': {
    task: require('zkflow-angular/src/tasks/sequence'),
    enabled: true,
    dependencies: [],
    sequence: [
      ['test']
    ],
    mode: {
      env: 'prod',
      watch: false
    }
  },
  css: {
    task: require('zkflow-angular/src/tasks/css'),
    enabled: true,
    dependencies: [],
    globs: [
      'src/index.scss',
      'src/**/_styles/*.{scss,sass}',
      'src/**/_styles/**/*.{scss,sass}'
    ],
    globsOptions: undefined,
    outputDirSuffix: '',
    cssGlobbing: {
      extensions: ['.sass', '.scss'],
      scssImportPath: {
        leading_underscore: false,
        filename_extension: false
      }
    },
    autoprefixer: {
      browsers: ['last 2 versions', 'ie 9'],
      cascade: false
    },
    sass: undefined,
    sourcemapsInit: undefined,
    sourcemapsWrite: undefined,
    cssoStructureMinimization: undefined,
    sassdoc: {
      dest: 'docs/sass/'
    }
  },
  default: {
    task: require('zkflow-angular/src/tasks/sequence'),
    enabled: true,
    dependencies: [],
    sequence: [
      'clean', ['inject', 'assets', 'lint-js', 'test'],
      'webserver'
    ],
    mode: undefined
  },
  e2e: {
    task: require('zkflow-angular/src/tasks/protractor'),
    enabled: true,
    dependencies: ['webdriver-update', 'assemble'],
    globs: [
      'e2e/features/*.feature',
      'e2e/features/**/*.feature'
    ],
    globsOptions: undefined
    customConfigFiles: false,
    configFile: 'protractor.conf.js',
    watchConfigFile: 'protractor.watch.conf.js'
  },
  inject: {
    task: require('zkflow-angular/src/tasks/inject'),
    enabled: true,
    dependencies: ['js', 'css'],
    globs: 'src/index.html',
    globsOptions: undefined
    injectablesGlobs: [
      'index*.js',
      'index*.css'
    ],
    injectablesGlobsOptions: {
      read: false
    },
    headInjectablesGlobs: undefined,
    absolute: true,
    prodAngularMainModuleName: 'app',
    devAngularMainModuleName: 'appDev',
    testAngularMainModuleName: 'appTest',
    minifyHtml: {
      empty: true,
      spare: true,
      quotes: true
    }
  },
  js: {
    task: require('zkflow-task-browserify'),
    enabled: true,
    dependencies: ['templates'],
    browserifyTransforms: [
      require('browserify-ngannotate')
    ]
  },
  'lint-js': {
    task: require('zkflow-task-eslint'),
    enabled: true,
    dependencies: [],
    eslint: {
      rules: {
        quotes: [2, 'single'],
        semi: [2, 'always'],
        eqeqeq: 2,
        strict: 2,
        'vars-on-top': 2,
        'comma-style': 2,
        indent: [2, 2],
        'linebreak-style': [2, 'unix'],
        'one-var': [2, 'never'],
        'no-trailing-spaces': 2,
        'no-multiple-empty-lines': [2, { 'max': 2, 'maxBOF': 0, 'maxEOF': 0 }],
        camelcase: [2, { properties: 'never' }],
        'comma-spacing': 2,
        'key-spacing': 2,
        'object-curly-spacing': [2, 'always']
      },
      env: {
        'commonjs': true,
        'browser': true,
        'jasmine': true
      },
      extends: 'eslint:recommended'
    }
  },
  test: {
    task: require('zkflow-task-karma'),
    enabled: true,
    dependencies: ['templates'],
    browsers: ['PhantomJS'],
    plugins: [require('karma-phantomjs-launcher')]
  }
}
```

### output dirs map

You can pass output dirs map object to init function.
This object maps current environment to output dir.

```JavaScript
require('zkflow-angular').init(options, outputDirsMap);
```

#### Default output dirs map

```
{
  prod: 'dist/',
  test: 'test/',
  dev: 'dev/'
}
```

### mode

You can retrieve mode object from zkflow

```JavaScript
var mode = require('zkflow-angular').mode;
```

This object is shared across all tasks and it define mode of operation.

Default mode

```JavaScript
{
  env: 'dev',
  watch: true,
  angularMainModuleProdFallback: false
}
```

Some of the mode properties can be changed on run by environment variables

```Shell
ZKFLOW_ENV=prod ZKFLOW_WATCH=false ./node_modules/.bin/gulp css
```

which is equivalent to

```Shell
bamboo_ZKFLOW_ENV=prod bamboo_ZKFLOW_WATCH=false ./node_modules/.bin/gulp css
```

Some tasks overwrites mode

Sponsors
--------

[<img alt="Street Team" src="http://zaklinaczekodu.com/_assets/streetteam.svg" width="200">](http://getstreetteam.com)

[<img alt="Zaklinacze Kodu" src="http://zaklinaczekodu.com/_assets/logo.svg" width="200">](http://zaklinaczekodu.com)
