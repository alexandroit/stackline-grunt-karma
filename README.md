# @stackline/grunt-karma

> grunt plugin for karma test runner.

[![npm version](https://img.shields.io/npm/v/@stackline/grunt-karma.svg?style=flat-square)](https://www.npmjs.com/package/@stackline/grunt-karma)
[![license](https://img.shields.io/npm/l/@stackline/grunt-karma.svg?style=flat-square)](https://github.com/alexandroit/stackline-grunt-karma)
[![GitHub repository](https://img.shields.io/badge/GitHub-alexandroit%2Fstackline-grunt-karma-181717?style=flat-square&logo=github)](https://github.com/alexandroit/stackline-grunt-karma)
[![Docs](https://img.shields.io/badge/docs-alexandro.net-0f766e?style=flat-square)](https://alexandro.net/docs/vanilla/grunt-karma/)
[![Reddit community](https://img.shields.io/badge/community-r%2FStackline-ff4500?style=flat-square&logo=reddit&logoColor=white)](https://www.reddit.com/r/Stackline/)

**[Documentation](https://alexandro.net/docs/vanilla/grunt-karma/)** | **[npm](https://www.npmjs.com/package/@stackline/grunt-karma)** | **[Issues](https://github.com/alexandroit/stackline-grunt-karma/issues)** | **[Repository](https://github.com/alexandroit/stackline-grunt-karma)**

**Current package version:** `1.0.1`

---

## Why this package?

`@stackline/grunt-karma` is the Stackline-maintained distribution of `grunt-karma@4.0.2`. It is an independent continuation of [grunt-karma](https://github.com/karma-runner/grunt-karma); original authors and licenses remain credited below.

## Compatibility

| Item | Value |
| :--- | :--- |
| Package | `@stackline/grunt-karma@1.0.1` |
| API target | `grunt-karma@4.0.2` |
| Supported Node.js | `See supported framework requirements` |
| License | `MIT` |
| Main entry | `tasks/grunt-karma.js` |
| Runtime dependencies | `lodash` |
| Peer dependencies | `grunt >=0.4.x, karma ^4.0.0 \|\| ^5.0.0 \|\| ^6.0.0` |

## Installation

```bash
npm install @stackline/grunt-karma
```

Preserve existing imports and plugin resolution with an npm alias:

```bash
npm install grunt-karma@npm:@stackline/grunt-karma
```

## Usage and API reference

### grunt-karma




> Grunt plugin for [Karma](https://github.com/karma-runner/karma)

This current version uses `karma@^3.0.0`. For using older versions see the
old releases of grunt-karma.

## Getting Started
From the same directory as your project's Gruntfile and package.json, install
karma and grunt-karma with the following commands:

```bash
$ npm install karma --save-dev
$ npm install @stackline/grunt-karma --save-dev
```

Once that's done, add this line to your project's Gruntfile:

```js
grunt.loadNpmTasks('@stackline/grunt-karma');
```

## Config
Inside your `Gruntfile.js` file, add a section named `karma`, containing
any number of configurations for running karma. You can either put your
config in a [karma config file] or leave it all in your Gruntfile (recommended).

### Here's an example that points to the config file:

```js
karma: {
  unit: {
    configFile: 'karma.conf.js'
  }
}
```

### Here's an example that puts the config in the Gruntfile:

```js
karma: {
  unit: {
    options: {
      files: ['test/**/*.js']
    }
  }
}
```

You can override any of the config file's settings by putting them
directly in the Gruntfile:

```js
karma: {
  unit: {
    configFile: 'karma.conf.js',
    port: 9999,
    singleRun: true,
    browsers: ['PhantomJS'],
    logLevel: 'ERROR'
  }
}
```

To change the `logLevel` in the grunt config file instead of the karma config, use one of the following strings:
`OFF`, `ERROR`, `WARN`, `INFO`, `DEBUG`

The `files` option can be extended "per-target" in the typical way
Grunt handles [files][grunt-config-files]:

```js
karma: {
  options: {
    files: ['lib/**/*.js']
  },
  unit: {
    files: [
      { src: ['test/**/*.js'] }
    ]
  }
}
```

When using the "Grunt way" of specifying files, you can also extend the
file objects with the options [supported by karma][karma-config-files]:

```js
karma: {
  unit: {
    files: [
      { src: ['test/**/*.js'], served: true },
      { src: ['lib/**/*.js'], served: true, included: false }
    ]
  }
}
```

### Config with Grunt Template Strings in `files`

When using template strings in the `files` option, the results will flattened. Therefore, if you include a variable that includes an array, the array will be flattened before being passed to Karma.

Example:

```js
meta: {
  jsFiles: ['jquery.js','angular.js']
},
karma: {
  options: {
    files: ['<%= meta.jsFiles %>','angular-mocks.js','**/*-spec.js']
  }
}
```

## Sharing Configs
If you have multiple targets, it may be helpful to share common
configuration settings between them. Grunt-karma supports this by
using the `options` property:

```js
karma: {
  options: {
    configFile: 'karma.conf.js',
    port: 9999,
    browsers: ['Chrome', 'Firefox']
  },
  continuous: {
    singleRun: true,
    browsers: ['PhantomJS']
  },
  dev: {
    reporters: 'dots'
  }
}
```

In this example the `continuous` and `dev` targets will both use
the `configFile` and `port` specified in the `options`. But
the `continuous` target will override the browser setting to use
PhantomJS, and also run as a singleRun. The `dev` target will simply
change the reporter to dots.

## Running tests
There are three ways to run your tests with karma:

### Karma Server with Auto Runs on File Change
Setting the `autoWatch` option to true will instruct karma to start
a server and watch for changes to files, running tests automatically:

```js
karma: {
  unit: {
    configFile: 'karma.conf.js',
    autoWatch: true
  }
}
```
Now run `$ grunt karma`

### Karma Server with Grunt Watch
Many Grunt projects watch several types of files using [grunt-contrib-watch].
Config karma like usual (without the autoWatch option), and add
`background:true`:

```js
karma: {
  unit: {
    configFile: 'karma.conf.js',
    background: true,
    singleRun: false
  }
}
```
The `background` option will tell grunt to run karma in a child process
so it doesn't block subsequent grunt tasks.

The `singleRun: false` option will tell grunt to keep the karma server up
after a test run.

Config your `watch` task to run the karma task with the `:run` flag. For example:

```js
watch: {
  //run unit tests with karma (server needs to be already running)
  karma: {
    files: ['app/js/**/*.js', 'test/browser/**/*.js'],
    tasks: ['karma:unit:run'] //NOTE the :run flag
  }
},
```

In your terminal window run `$ grunt karma:unit:start watch`, which starts the
karma server and the watch task. Now when grunt watch detects a change to
one of your watched files, it will run the tests specified in the `unit`
target using the already running karma server. This is the preferred method
for development.

### Single Run
Keeping a browser window & karma server running during development is
productive, but not a good solution for build processes. For that reason karma
provides a "continuous integration" mode, which will launch the specified
browser(s), run the tests, and close the browser(s). It also supports running
tests in [PhantomJS], a headless webkit browser which is great for running tests as part of a build. To run tests in continous integration mode just add the `singleRun` option:

```js
karma: {
  unit: {
    configFile: 'config/karma.conf.js',
  },
  //continuous integration mode: run tests once in PhantomJS browser.
  continuous: {
    configFile: 'config/karma.conf.js',
    singleRun: true,
    browsers: ['PhantomJS']
  },
}
```

The build would then run `grunt karma:continuous` to start PhantomJS,
run tests, and close PhantomJS.

## Using additional client.args
You can pass arbitrary `client.args` through the commandline like this:

```bash
$ grunt karma:dev watch --grep=mypattern
```


## License
MIT License

[karma-config-file]: http://karma-runner.github.com/latest/config/configuration-file.html
[karma-config-files]: http://karma-runner.github.io/latest/config/files.html
[grunt-config-files]: http://gruntjs.com/configuring-tasks#files
[grunt-contrib-watch]: https://github.com/gruntjs/grunt-contrib-watch
[PhantomJS]: http://phantomjs.org/
[karma-mocha]: https://github.com/karma-runner/karma-mocha

## Credits and original authors

- Original project: [grunt-karma](https://github.com/karma-runner/grunt-karma).
- Dave Geddes.
- Timo Tijhof.
- johnjbarton.
- Julian Motz.
- Michał Gołębiowski-Owczarek.
- XhmikosR.
- Mark Ethan Trostler.
- dsuckau.
- Greenkeeper.
- James Ford.
- James Forrester.
- Jeremy Vinai.
- Jonas Pommerening.
- Jonny Arnold.
- Julian.
- Luis Almeida.
- Matt Dean.
- Max Riveiro.
- Mike Dimmick.
- Nicolas Breitwieser.
- Olivier Amblet.
- Pascal Precht.
- Robin Hu.
- Robin Liang.
- Roman Morozov.
- Sahat Yalkabov.
- Valentin Hervieu.
- Vaughan Hilts.
- Vlad Filippov.
- Vojta Jina.
- enigmak.
- facboy.
- jiverson.
- joshrtay.
- kolesnik.
- Adrian.
- m7r.
- Alexander Slansky.
- Alexey Kucherenko.
- Chris Gross.
- Chris Wren.
- Christian Reed.
- Christoph Kraemer.
- Daniel Herman.
- Eddie Monge.
- Copyright (c) 2013 Dave Geddes.
- Stackline maintenance: [Alexandro Paixao Marques](https://www.linkedin.com/in/aleinfo/) and [Stackline contributors](https://github.com/alexandroit).

Original copyright, license notices and contributor acknowledgements remain part of this distribution. Stackline maintenance does not replace authorship of the original work.

## Community and Links

- [Stackline website](https://alexandro.net/)
- [GitHub projects](https://github.com/alexandroit)
- [npm packages](https://www.npmjs.com/~alex360qc)
- [Reddit community — r/Stackline](https://www.reddit.com/r/Stackline/)
- [Maintainer LinkedIn](https://www.linkedin.com/in/aleinfo/)

Use this repository's issue tracker for reproducible bugs and feature requests. Join r/Stackline for examples, usage questions and release discussions.
