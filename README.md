# @pagopa/io-react-native-nodelibs

This package provides **React Native** compatible implementations of Node core modules like `stream`, `crypto` and `http` avoiding the use of [rn-nodeify](https://github.com/tradle/rn-nodeify/) which is now deprecated.

This is a fork of [node-libs-react-native](https://github.com/parshap/node-libs-react-native) which introduces some improvements and fixes compatible with new versions of node.

## Installation

```sh
yarn add @pagopa/io-react-native-nodelibs
```

## Usage

This package exports a mapping of absolute paths to each module implementation, keyed by module name. Modules without React Native compatible implementations are `null`.

These modules can be used with React Native Packager's `metro.config.js` or Webpack's `resolve.alias`.

### Usage with React Native Packager

Add a `metro.config.js` file in the root directory of your React Native project and set `resolver.extraNodeModules`:

```js
// metro.config.js
module.exports = {
  resolver: {
    extraNodeModules: require('@pagopa/io-react-native-nodelibs'),
  },
};
```

### Globals

Node has certain globals that modules may expect, such as `Buffer` or `process`. React Native does not provide these globals. The [`@pagopa/io-react-native-nodelibs/globals`][globals] module in this package will shim the global environment to add these globals. Just require (or import) this module in your app before anything else.

[globals]: ./globals.js

```js
require('@pagopa/io-react-native-nodelibs/globals');
// ...
require('./app.js');
```

## Modules

The following are the module implementations provided by this package.

| Module | RN-compatible |
|:--------:|:----------------------:|
| assert | [defunctzombie/commonjs-assert](https://github.com/defunctzombie/commonjs-assert) |
| buffer | [feross/buffer](https://github.com/feross/buffer) |
| child_process | --- |
| cluster | --- |
| console | [Raynos/console-browserify](https://github.com/Raynos/console-browserify) |
| constants | [juliangruber/constants-browserify](https://github.com/juliangruber/constants-browserify) |
| crypto | [mvayngrib/react-native-crypto](https://github.com/mvayngrib/react-native-crypto) |
| dgram | --- |
| dns | --- |
| domain | [bevry/domain-browser](https://github.com/bevry/domain-browser) |
| events | [Gozala/events](https://github.com/Gozala/events) |
| fs | [itinance/react-native-fs](https://github.com/itinance/react-native-fs) |
| http | [jhiesey/stream-http](https://github.com/jhiesey/stream-http) |
| https | [substack/https-browserify](https://github.com/substack/https-browserify) |
| module | --- |
| net | --- |
| os | [CoderPuppy/os-browserify](https://github.com/CoderPuppy/os-browserify) |
| path | [substack/path-browserify](https://github.com/substack/path-browserify) |
| process | [shtylman/node-process](https://github.com/shtylman/node-process) |
| punycode | [bestiejs/punycode.js](https://github.com/bestiejs/punycode.js) |
| querystring | [mike-spainhower/querystring](https://github.com/mike-spainhower/querystring) |
| readline | --- |
| repl | --- |
| stream | [nodejs/readable-stream](https://github.com/nodejs/readable-stream) |
| string_decoder | [rvagg/string_decoder](https://github.com/rvagg/string_decoder) |
| sys | [defunctzombie/node-util](https://github.com/defunctzombie/node-util) |
| timers | [jryans/timers-browserify](https://github.com/jryans/timers-browserify) |
| tls | --- |
| tty | [substack/tty-browserify](https://github.com/substack/tty-browserify) |
| url | [defunctzombie/node-url](https://github.com/defunctzombie/node-url) |
| util | [defunctzombie/node-util](https://github.com/defunctzombie/node-util) |
| vm | --- |
| zlib | [devongovett/browserify-zlib](https://github.com/devongovett/browserify-zlib) |
