# parallel-protractor

> Running parallel end 2 end tests from the same spec file using Protractor

[![NPM][parallel-protractor-icon] ][parallel-protractor-url]

[![Build status][parallel-protractor-ci-image] ][parallel-protractor-ci-url]
[![semantic-release][semantic-image] ][semantic-url]

[parallel-protractor-icon]: https://nodei.co/npm/parallel-protractor.png?downloads=true
[parallel-protractor-url]: https://npmjs.org/package/parallel-protractor
[parallel-protractor-ci-image]: https://travis-ci.org/kensho/parallel-protractor.png?branch=master
[parallel-protractor-ci-url]: https://travis-ci.org/kensho/parallel-protractor
[semantic-image]: https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg
[semantic-url]: https://github.com/semantic-release/semantic-release

**WARNING** still work in progress, some dependency loading issues.

## Install and use

```
npm i -D parallel-protractor
```

Then, instead the command `protractor conf.js` run the command to load `parallel-protractor`
first

```json
{
  "scripts": {
    "test": "protractor conf.js",
    "test-in-parallel": "node -r parallel-protractor node_modules/.bin/protractor conf.js"
  }
}
```

If `conf.js` is not present it will try using `protractor.conf.js`

By default the script assumes a suite called `one`. You can override this default by specifying a `SUITE` environment variable.

You may also specify a `PROTRACTOR_CONFIG_PATH` environment variable to point to a specific Protractor config file.

## Sample config

```
exports.config = {
  framework: 'mocha',
  seleniumAddress: 'http://localhost:4444/wd/hub',
  suites: {
    one: 'spec.js' // all tests in single file
  },
  suite: 'one', // default suite to run
  mochaOpts: {
    ui: 'bdd',
    reporter: 'spec',
    slow: 5000
  },
  capabilities: {
    browserName: 'firefox', // chrome
    shardTestFiles: true,
    maxInstances: 2
  }
}
```

## Test

See the `/test/one` folder for a full usage example.

## Why?

If you have a large file with long running end to end tests, you can refactor the long file into the smaller separate physical files. The you can 
[configure parallel tests](http://blog.yodersolutions.com/run-protractor-tests-in-parallel/).
Or you can just create "virtual" spec files on the fly using `parallel-protractor`! It overrides
the Node `require` function called from Protractor and tells it that there is a file for each
`describe` block.

## License

Author: Kensho &copy; 2016

* [@kensho](https://twitter.com/kensho)
* [kensho.com](http://kensho.com)

Support: if you find any problems with this library,
[open issue](https://github.com/kensho/parallel-protractor/issues) on Github

The MIT License (MIT)

Copyright (c) 2016 Kensho

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
