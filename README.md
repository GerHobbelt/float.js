## float.js

A little mirror class for introspecting the bit-patterns of JS numbers using typed arrays.

Example:

``` javascript
Math.PI.introspect().mantissa;     //             "1001001000011111101101010100010001000010110100011000"
Math.E.introspect().exponent;      //  "10000000000"
(9.0).introspect().toBitString();  // "0100000000100010000000000000000000000000000000000000000000000000"
(-Math.PI).introspect().negative;  // true
```

Interactively explore at [http://dherman.github.com/float.js](http://dherman.github.com/float.js).

### How it works

[Internally](https://github.com/dherman/float.js/blob/master/float.js), this puts the number in a single-element `Float64Array` [typed array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Typed_arrays) and gets its `buffer` to read the value’s raw bits:

```javascript
(new Float64Array([n])).buffer
```

Then it converts that buffer to a string of `"1"`s and `"0"`s by viewing the buffer as a `Uint8Array` and mapping each viewed byte to a binary string with `.toString(2)`. Finally, it creates properties like `exponent` and `mantissa` by using `[]` array indexing, `.substring`, and `.slice` to extract the relevant bits.

### License

Copyright © 2012 Dave Herman

Licensed under the [MIT License](http://mit-license.org).
