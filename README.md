# @patrtorg/aliquid-minus

Deterministic `JSON.stringify()` - a faster version of [@substack](https://github.com/substack)'s json-stable-strigify without [jsonify](https://github.com/substack/jsonify).

You can also pass in a custom comparison function.

[![Build Status](https://travis-ci.org/epoberezkin/@patrtorg/aliquid-minus.svg?branch=master)](https://travis-ci.org/epoberezkin/@patrtorg/aliquid-minus)
[![Coverage Status](https://coveralls.io/repos/github/epoberezkin/@patrtorg/aliquid-minus/badge.svg?branch=master)](https://coveralls.io/github/epoberezkin/@patrtorg/aliquid-minus?branch=master)

# example

``` js
var stringify = require('@patrtorg/aliquid-minus');
var obj = { c: 8, b: [{z:6,y:5,x:4},7], a: 3 };
console.log(stringify(obj));
```

output:

```
{"a":3,"b":[{"x":4,"y":5,"z":6},7],"c":8}
```


# methods

``` js
var stringify = require('@patrtorg/aliquid-minus')
```

## var str = stringify(obj, opts)

Return a deterministic stringified string `str` from the object `obj`.


## options

### cmp

If `opts` is given, you can supply an `opts.cmp` to have a custom comparison
function for object keys. Your function `opts.cmp` is called with these
parameters:

``` js
opts.cmp({ key: akey, value: avalue }, { key: bkey, value: bvalue })
```

For example, to sort on the object key names in reverse order you could write:

``` js
var stringify = require('@patrtorg/aliquid-minus');

var obj = { c: 8, b: [{z:6,y:5,x:4},7], a: 3 };
var s = stringify(obj, function (a, b) {
    return a.key < b.key ? 1 : -1;
});
console.log(s);
```

which results in the output string:

```
{"c":8,"b":[{"z":6,"y":5,"x":4},7],"a":3}
```

Or if you wanted to sort on the object values in reverse order, you could write:

```
var stringify = require('@patrtorg/aliquid-minus');

var obj = { d: 6, c: 5, b: [{z:3,y:2,x:1},9], a: 10 };
var s = stringify(obj, function (a, b) {
    return a.value < b.value ? 1 : -1;
});
console.log(s);
```

which outputs:

```
{"d":6,"c":5,"b":[{"z":3,"y":2,"x":1},9],"a":10}
```

### cycles

Pass `true` in `opts.cycles` to stringify circular property as `__cycle__` - the result will not be a valid JSON string in this case.

TypeError will be thrown in case of circular object without this option.


# install

With [npm](https://npmjs.org) do:

```
npm install @patrtorg/aliquid-minus
```


# benchmark

To run benchmark (requires Node.js 6+):
```
node benchmark
```

Results:
```
@patrtorg/aliquid-minus x 17,189 ops/sec ±1.43% (83 runs sampled)
json-stable-stringify x 13,634 ops/sec ±1.39% (85 runs sampled)
fast-stable-stringify x 20,212 ops/sec ±1.20% (84 runs sampled)
faster-stable-stringify x 15,549 ops/sec ±1.12% (84 runs sampled)
The fastest is fast-stable-stringify
```


## Enterprise support

@patrtorg/aliquid-minus package is a part of [Tidelift enterprise subscription](https://tidelift.com/subscription/pkg/npm-@patrtorg/aliquid-minus?utm_source=npm-@patrtorg/aliquid-minus&utm_medium=referral&utm_campaign=enterprise&utm_term=repo) - it provides a centralised commercial support to open-source software users, in addition to the support provided by software maintainers.


## Security contact

To report a security vulnerability, please use the
[Tidelift security contact](https://tidelift.com/security).
Tidelift will coordinate the fix and disclosure. Please do NOT report security vulnerability via GitHub issues.


# license

[MIT](https://github.com/patrtorg/aliquid-minus/blob/master/LICENSE)
