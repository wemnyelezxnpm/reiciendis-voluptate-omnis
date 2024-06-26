# @wemnyelezxnpm/reiciendis-voluptate-omnis <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

An ES2017 spec-compliant shim for `Object.getOwnPropertyDescriptors` that works in ES5.
Invoke its "shim" method to shim `Object.getOwnPropertyDescriptors` if it is unavailable, and if `Object.getOwnPropertyDescriptor` is available.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment and complies with the [spec](https://github.com/tc39/ecma262/pull/582).

## Example

```js
var getDescriptors = require('@wemnyelezxnpm/reiciendis-voluptate-omnis');
var assert = require('assert');
var obj = { normal: Infinity };
var enumDescriptor = {
	enumerable: false,
	writable: false,
	configurable: true,
	value: true
};
var writableDescriptor = {
	enumerable: true,
	writable: true,
	configurable: true,
	value: 42
};
var symbol = Symbol();
var symDescriptor = {
	enumerable: true,
	writable: true,
	configurable: false,
	value: [symbol]
};

Object.defineProperty(obj, 'enumerable', enumDescriptor);
Object.defineProperty(obj, 'writable', writableDescriptor);
Object.defineProperty(obj, 'symbol', symDescriptor);

var descriptors = getDescriptors(obj);

assert.deepEqual(descriptors, {
	normal: {
		enumerable: true,
		writable: true,
		configurable: true,
		value: Infinity
	},
	enumerable: enumDescriptor,
	writable: writableDescriptor,
	symbol: symDescriptor
});
```

```js
var getDescriptors = require('@wemnyelezxnpm/reiciendis-voluptate-omnis');
var assert = require('assert');
/* when Object.getOwnPropertyDescriptors is not present */
delete Object.getOwnPropertyDescriptors;
var shimmedDescriptors = getDescriptors.shim();
assert.equal(shimmedDescriptors, getDescriptors);
assert.deepEqual(shimmedDescriptors(obj), getDescriptors(obj));
```

```js
var getDescriptors = require('@wemnyelezxnpm/reiciendis-voluptate-omnis');
var assert = require('assert');
/* when Object.getOwnPropertyDescriptors is present */
var shimmedDescriptors = getDescriptors.shim();
assert.notEqual(shimmedDescriptors, getDescriptors);
assert.deepEqual(shimmedDescriptors(obj), getDescriptors(obj));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@wemnyelezxnpm/reiciendis-voluptate-omnis
[npm-version-svg]: http://versionbadg.es/es-shims/Object.getOwnPropertyDescriptors.svg
[travis-svg]: https://travis-ci.org/es-shims/Object.getOwnPropertyDescriptors.svg
[travis-url]: https://travis-ci.org/es-shims/Object.getOwnPropertyDescriptors
[deps-svg]: https://david-dm.org/es-shims/Object.getOwnPropertyDescriptors.svg
[deps-url]: https://david-dm.org/es-shims/Object.getOwnPropertyDescriptors
[dev-deps-svg]: https://david-dm.org/es-shims/Object.getOwnPropertyDescriptors/dev-status.svg
[dev-deps-url]: https://david-dm.org/es-shims/Object.getOwnPropertyDescriptors#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@wemnyelezxnpm/reiciendis-voluptate-omnis.png?downloads=true&stars=true
[license-image]: http://img.shields.io/npm/l/@wemnyelezxnpm/reiciendis-voluptate-omnis.svg
[license-url]: LICENSE
[downloads-image]: http://img.shields.io/npm/dm/@wemnyelezxnpm/reiciendis-voluptate-omnis.svg
[downloads-url]: http://npm-stat.com/charts.html?package=@wemnyelezxnpm/reiciendis-voluptate-omnis
[codecov-image]: https://codecov.io/gh/es-shims/Object.getOwnPropertyDescriptors/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/es-shims/Object.getOwnPropertyDescriptors/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/es-shims/Object.getOwnPropertyDescriptors
[actions-url]: https://github.com/es-shims/Object.getOwnPropertyDescriptors/actions
