<!--

@license Apache-2.0

Copyright (c) 2025 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# range

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Compute the [range][range] along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.

<section class="intro">

The [**range**][range] is defined as the difference between the maximum and minimum values.

</section>

<!-- /.intro -->



<section class="usage">

## Usage

To use in Observable,

```javascript
range = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/stats-range@umd/browser.js' )
```

To vendor stdlib functionality and avoid installing dependency trees for Node.js, you can use the UMD server build:

```javascript
var range = require( 'path/to/vendor/umd/stats-range/index.js' )
```

To include the bundle in a webpage,

```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/stats-range@umd/browser.js"></script>
```

If no recognized module system is present, access bundle contents via the global scope:

```html
<script type="text/javascript">
(function () {
    window.range;
})();
</script>
```

#### range( x\[, options] )

Computes the [range][range] along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.

```javascript
var array = require( '@stdlib/ndarray-array' );

var x = array( [ -1.0, 2.0, -3.0 ] );

var y = range( x );
// returns <ndarray>[ 5.0 ]
```

The function has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor]. Must have a real-valued or "generic" [data type][@stdlib/ndarray/dtypes].
-   **options**: function options (_optional_).

The function accepts the following options:

-   **dims**: list of dimensions over which to perform a reduction. If not provided, the function performs a reduction over all elements in a provided input [ndarray][@stdlib/ndarray/ctor].
-   **dtype**: output ndarray [data type][@stdlib/ndarray/dtypes]. Must be a real-valued or "generic" [data type][@stdlib/ndarray/dtypes].
-   **keepdims**: boolean indicating whether the reduced dimensions should be included in the returned [ndarray][@stdlib/ndarray/ctor] as singleton dimensions. Default: `false`.

By default, the function performs a reduction over all elements in a provided input [ndarray][@stdlib/ndarray/ctor]. To perform a reduction over specific dimensions, provide a `dims` option.

```javascript
var array = require( '@stdlib/ndarray-array' );

var x = array( [ -1.0, 2.0, -3.0, 4.0 ], {
    'shape': [ 2, 2 ],
    'order': 'row-major'
});
// returns <ndarray>[ [ -1.0, 2.0 ], [ -3.0, 4.0 ] ]

var y = range( x, {
    'dims': [ 0 ]
});
// returns <ndarray>[ 2.0, 2.0 ]

y = range( x, {
    'dims': [ 1 ]
});
// returns <ndarray>[ 3.0, 7.0 ]

y = range( x, {
    'dims': [ 0, 1 ]
});
// returns <ndarray>[ 7.0 ]
```

By default, the function excludes reduced dimensions from the output [ndarray][@stdlib/ndarray/ctor]. To include the reduced dimensions as singleton dimensions, set the `keepdims` option to `true`.

```javascript
var array = require( '@stdlib/ndarray-array' );

var x = array( [ -1.0, 2.0, -3.0, 4.0 ], {
    'shape': [ 2, 2 ],
    'order': 'row-major'
});
// returns <ndarray>[ [ -1.0, 2.0 ], [ -3.0, 4.0 ] ]

var y = range( x, {
    'dims': [ 0 ],
    'keepdims': true
});
// returns <ndarray>[ [ 2.0, 2.0 ] ]

y = range( x, {
    'dims': [ 1 ],
    'keepdims': true
});
// returns <ndarray>[ [ 3.0 ], [ 7.0 ] ]

y = range( x, {
    'dims': [ 0, 1 ],
    'keepdims': true
});
// returns <ndarray>[ [ 7.0 ] ]
```

By default, the function returns an [ndarray][@stdlib/ndarray/ctor] having a [data type][@stdlib/ndarray/dtypes] determined by the function's output data type [policy][@stdlib/ndarray/output-dtype-policies]. To override the default behavior, set the `dtype` option.

```javascript
var getDType = require( '@stdlib/ndarray-dtype' );
var array = require( '@stdlib/ndarray-array' );

var x = array( [ -1.0, 2.0, -3.0 ], {
    'dtype': 'generic'
});

var y = range( x, {
    'dtype': 'float64'
});
// returns <ndarray>[ 5.0 ]

var dt = String( getDType( y ) );
// returns 'float64'
```

#### range.assign( x, out\[, options] )

Computes the [range][range] along one or more [ndarray][@stdlib/ndarray/ctor] dimensions and assigns results to a provided output [ndarray][@stdlib/ndarray/ctor].

```javascript
var array = require( '@stdlib/ndarray-array' );
var zeros = require( '@stdlib/ndarray-zeros' );

var x = array( [ -1.0, 2.0, -3.0 ] );
var y = zeros( [] );

var out = range.assign( x, y );
// returns <ndarray>[ 5.0 ]

var bool = ( out === y );
// returns true
```

The method has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor]. Must have a real-valued or "generic" [data type][@stdlib/ndarray/dtypes].
-   **out**: output [ndarray][@stdlib/ndarray/ctor].
-   **options**: function options (_optional_).

The method accepts the following options:

-   **dims**: list of dimensions over which to perform a reduction. If not provided, the function performs a reduction over all elements in a provided input [ndarray][@stdlib/ndarray/ctor].

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   Setting the `keepdims` option to `true` can be useful when wanting to ensure that the output [ndarray][@stdlib/ndarray/ctor] is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with ndarrays having the same shape as the input [ndarray][@stdlib/ndarray/ctor].
-   The output data type [policy][@stdlib/ndarray/output-dtype-policies] only applies to the main function and specifies that, by default, the function must return an [ndarray][@stdlib/ndarray/ctor] having the same [data type][@stdlib/ndarray/dtypes] as the input [ndarray][@stdlib/ndarray/ctor]. For the `assign` method, the output [ndarray][@stdlib/ndarray/ctor] is allowed to have any supported output [data type][@stdlib/ndarray/dtypes].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/random-uniform@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-dtype@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/stats-range@umd/browser.js"></script>
<script type="text/javascript">
(function () {

// Generate an array of random numbers:
var x = uniform( [ 5, 5 ], 0.0, 20.0 );
console.log( ndarray2array( x ) );

// Perform a reduction:
var y = range( x, {
    'dims': [ 0 ]
});

// Resolve the output array data type:
var dt = getDType( y );
console.log( dt );

// Print the results:
console.log( ndarray2array( y ) );

})();
</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/stats-range.svg
[npm-url]: https://npmjs.org/package/@stdlib/stats-range

[test-image]: https://github.com/stdlib-js/stats-range/actions/workflows/test.yml/badge.svg?branch=v0.1.0
[test-url]: https://github.com/stdlib-js/stats-range/actions/workflows/test.yml?query=branch:v0.1.0

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/stats-range/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/stats-range?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/stats-range.svg
[dependencies-url]: https://david-dm.org/stdlib-js/stats-range/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/stats-range/tree/deno
[deno-readme]: https://github.com/stdlib-js/stats-range/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/stats-range/tree/umd
[umd-readme]: https://github.com/stdlib-js/stats-range/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/stats-range/tree/esm
[esm-readme]: https://github.com/stdlib-js/stats-range/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/stats-range/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/stats-range/main/LICENSE

[@stdlib/ndarray/ctor]: https://github.com/stdlib-js/ndarray-ctor/tree/umd

[@stdlib/ndarray/dtypes]: https://github.com/stdlib-js/ndarray-dtypes/tree/umd

[@stdlib/ndarray/output-dtype-policies]: https://github.com/stdlib-js/ndarray-output-dtype-policies/tree/umd

[@stdlib/ndarray/base/broadcast-shapes]: https://github.com/stdlib-js/ndarray-base-broadcast-shapes/tree/umd

[range]: https://en.wikipedia.org/wiki/Range_%28statistics%29

</section>

<!-- /.links -->
