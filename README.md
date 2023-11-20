# @pagopa/react-native-nodelibs

This package provides **React Native** compatible implementations of Node core modules like `stream`, `crypto` and `http` avoiding the use of [rn-nodeify](https://github.com/tradle/rn-nodeify/) which is now deprecated.

This is a fork of [node-libs-react-native](https://github.com/parshap/node-libs-react-native) which introduces some improvements and fixes compatible with new versions of node.

`crypto.getRandomValues` is based on [react-native-get-random-values](https://github.com/LinusU/react-native-get-random-values#readme) native library. So you need to install it to be able to use `crypto`

## Installation

```sh
yarn add @pagopa/react-native-nodelibs

# If you need to use `crypto`
yarn add react-native-get-random-values
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
    extraNodeModules: require('@pagopa/react-native-nodelibs'),
  },
};
```

### Globals

Node has certain globals that modules may expect, such as `Buffer` or `process`. React Native does not provide these globals. The [`@pagopa/react-native-nodelibs/globals`][globals] module in this package will shim the global environment to add these globals. Just require (or import) this module in your app before anything else.

[globals]: ./globals.js

```js
require('@pagopa/react-native-nodelibs/globals');
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
| crypto | [See the next paragraph](#crypto-modules) |
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

### Crypto Modules

The crypto modules have been replaced by their JavaScript-based versions.
Below are the various modules implemented on `crypto`

| Crypto module | RN-compatible |
|:--------:|:----------------------:|
| getRandomValues | [react-native-get-random-values](https://github.com/LinusU/react-native-get-random-values) |
| createHash | [create-hash](https://github.com/browserify/createHash) |
| createHmac | [create-hmac](https://github.com/browserify/createHmac) |
| getHashes | [browserify-sign/algos](https://github.com/browserify/browserify-sign) |
| pbkdf2 | [pbkdf2](https://github.com/browserify/pbkdf2) |
| pbkdf2Sync | [pbkdf2](https://github.com/browserify/pbkdf2) |
| createCipher, createCipheriv, createDecipher, createDecipheriv, getCiphers, listCiphers | [browserify-cipher](https://github.com/browserify/browserify-cipher) |
| createDiffieHellmanGroup, getDiffieHellman, createDiffieHellman | [diffie-hellman](https://www.npmjs.com/package/diffie-hellman) |
| createSign, createVerify | [browserify-sign](https://github.com/browserify/browserify-sign) |
| createECDH | [create-ecdh](https://github.com/browserify/createECDH) |
| publicEncrypt, privateEncrypt, publicDecrypt | [public-encrypt](https://github.com/browserify/publicEncrypt) |
| randomFill, randomFillSync | [randomfill](https://github.com/browserify/randomfill) |
