# glob-stream [![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Coveralls Status][coveralls-image]][coveralls-url] [![Dependency Status][david-image]][david-url]


## Information

<table>
<tr>
<td>Package</td><td>glob-stream</td>
</tr>
<tr>
<td>Description</td>
<td>File system globs as a stream</td>
</tr>
<tr>
<td>Node Version</td>
<td>>= 0.9</td>
</tr>
</table>

This is a simple wrapper around node-glob to make it streamy.

## Usage

```javascript
var gs = require('glob-stream');

var stream = gs.create('./files/**/*.coffee', {options});

stream.on('data', function(file){
  // file has path, base, and cwd attrs
});
```

You can pass any combination of globs. One caveat is that you can not only pass a glob negation, you must give it at least one positive glob so it knows where to start. All given must match for the file to be returned.

### Options

- cwd
  - Default is `process.cwd()`
- base
  - Default is everything before a glob starts (see [glob-parent](https://github.com/es128/glob-parent))
- cwdbase
  - Default is `false`
  - When true it is the same as saying opt.base = opt.cwd
- allowEmpty
  - Default is `false`
  - If true, won't emit an error when a glob pointing at a single file fails to match
- Any through2 related options are documented in [through2](https://github.com/rvagg/through2)

This argument is passed directly to [node-glob](https://github.com/isaacs/node-glob) so check there for more options

#### Glob

```js
var stream = gs.create(['./**/*.js', '!./node_modules/**/*']);
```

Globs are executed in order, so negations should follow positive globs. For example:

```js
gulp.src(['!b*.js', '*.js'])
```

would not exclude any files, but this would

```js
gulp.src(['*.js', '!b*.js'])
```

#### Related

- [globby](https://github.com/sindresorhus/globby) - Non-streaming `glob` wrapper with support for multiple patterns.


[npm-url]: https://www.npmjs.com/package/glob-stream
[npm-image]: https://badge.fury.io/js/glob-stream.svg

[travis-url]: https://travis-ci.org/gulpjs/glob-stream
[travis-image]: https://travis-ci.org/gulpjs/glob-stream.svg?branch=master

[coveralls-url]: https://coveralls.io/r/gulpjs/glob-stream
[coveralls-image]: https://coveralls.io/repos/gulpjs/glob-stream/badge.svg

[david-url]: https://david-dm.org/gulpjs/glob-stream
[david-image]: https://david-dm.org/gulpjs/glob-stream.svg
