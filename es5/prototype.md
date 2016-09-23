## ES5的自訂物件類型及其method - 使用 prototype

#### 非自建物件類型的, 即`var obj ={};`, 可參考上一個章節的Object Literal Notation

### ES5, 自建物件類型的method宣告方式 以及static method/data:

物件的member成員若是function, 通常叫做method

**非static method:**
1. `Person.prototype.sayHello = function()`
2. in constructor:  
~~~ javascript
function Person (){  
  this.someData = 0;  
  this.testFun = function{  
  //can use this.someData to access
  }
}
~~~
**static method:**
`MyClass.method1 = function ()`. It has no relationship with an object instance of that constructor function [http://ithelp.ithome.com.tw/question/10128721](http://ithelp.ithome.com.tw/question/10128721)

**static property** 也可以透過一樣方式定義:`MyClass.staticProperty1 = "test"`

jQuery的library應該主要部份是純function, 部份是static method. e.g. `$('.jQueryButton')` 跟 `$.get()`

### Function的Prototype [進階]

參考: 

1. Function.prototype
[https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/prototype](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/prototype)
2. Inheritance and the prototype chain 
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain

example:
~~~ javascript
var o = { a: {name:"k1"}, m: function(b){ return this.a + 1; }};

var p = Object.create(o);// p is an object that inherits from o

p.a.name ="k2";console.log("p.a:", p.a); // { name: 'k2' } console.log("o.a:", p.a); // { name: 'k2' } !!!!

~~~

