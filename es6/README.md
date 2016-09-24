# JavaScript ES6 語法說明

**ES6 = ECMAScript 6 = ECMAScript 2015. **

ES6 還是未有直接support class的 private member當使用const/let等時, 且在node.js上, 則一定要運行在Strict Mode Code下, 即`use strict`. 不然會出現 Block-scoped declarations (let, const, function, class) not yet supported outside strict mode

ES6 如何在class上模擬private data/method:

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

## 其餘部份待補充
