# JavaScript ES6 語法說明

**ES6 = ECMAScript 6 = ECMAScript 2015. **

ES6 還是未有直接support class的 private member.

當使用const/let等時, 且在node.js上, 則一定要運行在Strict Mode Code下, 即`use strict`. 不然會出現 Block-scoped declarations (let, const, function, class) not yet supported outside strict mode

### ES6 如何在class上模擬private data/method:

1. [http://www.2ality.com/2016/01/private-data-classes.html](http://www.2ality.com/2016/01/private-data-classes.html)
2. [http://stackoverflow.com/questions/27849064/how-to-implement-private-method-in-es6-class-with-traceur](http://stackoverflow.com/questions/27849064/how-to-implement-private-method-in-es6-class-with-traceur)

上述兩個link都提到兩種方式WeakMap & Symbol.

### ES6裡的Prototype

`class` 本質上是prototype的syntactical sugar)的導入.  [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain]

Since ECMAScript 6, the [[Prototype]] is accessed using the accessors Object.getPrototypeOf() and Object.setPrototypeOf().

### let , const 為 block level 變數的關鍵字

~~~ javascript
if(true){
  var x = 1;
}
console.log(x); //1

if(true){
  let y = 2; //its lifetime is only in thie scope     
}
console.log(y); //exception, undefined
~~~

### shorthand syntax of Method definitions

Given the following code:
~~~ javascript
var obj = {
  foo: function() {},
  bar: function() {}
};
~~~

You are now able to shorten this to:
~~~ javascript
var obj = {
  foo() {},
  bar() {}
};
~~~

## 其餘部份待補充, 可先參考
[https://github.com/lukehoban/es6features](https://github.com/lukehoban/es6features)

上面網站裡的功能清單 *ES6 includes the following new features*:
- [arrows](https://github.com/lukehoban/es6features/blob/master/README.md#arrows)
- [classes](https://github.com/lukehoban/es6features/blob/master/README.md#classes)
- [enhanced object literals](https://github.com/lukehoban/es6features/blob/master/README.md#enhanced-object-literals)
- [template strings](https://github.com/lukehoban/es6features/blob/master/README.md#template-strings)
- [destructuring](https://github.com/lukehoban/es6features/blob/master/README.md#destructuring)
- [default + rest + spread](https://github.com/lukehoban/es6features/blob/master/README.md#default--rest--spread)
- [let + const](https://github.com/lukehoban/es6features/blob/master/README.md#let--const)
- [iterators + for..of](https://github.com/lukehoban/es6features/blob/master/README.md#iterators--forof)
- [generators](https://github.com/lukehoban/es6features/blob/master/README.md#generators)
- [unicode](https://github.com/lukehoban/es6features/blob/master/README.md#unicode)
- [modules](https://github.com/lukehoban/es6features/blob/master/README.md#modules)
- [module loaders](https://github.com/lukehoban/es6features/blob/master/README.md#module-loaders)
- [map + set + weakmap + weakset](https://github.com/lukehoban/es6features/blob/master/README.md#map--set--weakmap--weakset)
- [proxies](https://github.com/lukehoban/es6features/blob/master/README.md#proxies)
- [symbols](https://github.com/lukehoban/es6features/blob/master/README.md#symbols)
- [subclassable built-ins](https://github.com/lukehoban/es6features/blob/master/README.md#subclassable-built-ins)
- [promises](https://github.com/lukehoban/es6features/blob/master/README.md#promises)
- [math + number + string + array + object APIs](https://github.com/lukehoban/es6features/blob/master/README.md#math--number--string--array--object-apis)
- [binary and octal literals](https://github.com/lukehoban/es6features/blob/master/README.md#binary-and-octal-literals)
- [reflect api](https://github.com/lukehoban/es6features/blob/master/README.md#reflect-api)
- [tail calls](https://github.com/lukehoban/es6features/blob/master/README.md#tail-calls)
