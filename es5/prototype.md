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
2. Inheritance and the prototype chain, 使用 `Object.create`去建立一個新物件並且其prototype為傳進去的物件.
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain

重點Notes:
1. 不管是property或是method, access時若果當前type沒有找到此property/method, 都會往它的prototype指到的物件去找，遞迴的一直找到為止/或找到Object都沒有
2. 為什麼常見自訂object type的method要用`Car.prototype.autopilot`此寫法，是因為在new Car()時, 它會copy這個Car(<-一function object)的prototype到新建的prototype property.
3. Object.create的概念

example1: 使用 `Object.create(某物件)`;並且繼承的人可以改到obj的property.

~~~ javascript
var o = {
  a: {name:"k1"},
  m: function(b){
    return this.a + 1;
  }
};

var p = Object.create(o);
// p is an object that inherits from o

p.a.name ="k2";
console.log("p.a:", p.a); // { name: 'k2' }

console.log("o.a:", p.a); // { name: 'k2' }
//有改到o.a !!代表Object.create的inherit跟一般class based的語言其實意義不一樣
~~~

**example2**: 使用 `Object.create(某Function/type.prototype)`;

1 這篇有提到 多型polymorphism & factory pattern
http://stackoverflow.com/questions/34525517/angularjs-how-to-achieve-polymorphism-dependency-injection-best-practices
~~~ javascript
function Car(name,year, model){
   Auto.call(this,name,year);
   this.model=model;
}
Car.prototype = Object.create(Auto.prototype);
~~~

2 這篇有提到 多型polymorphism
http://stackoverflow.com/questions/9850892/should-i-use-polymorphism-in-javascript
~~~ javascript

function Circle() {
  // constructor;
}

Circle.prototype = Object.create(Shape.prototype);
Circle.prototype.printSurface = function() {
  // Circle implementation
}

var obj = new Circle();

if (obj instanceof Shape) {
    // do something with a shape object
}
~~~

**example3**: 不使用`Object.create`, 直接指定某Function/Type其Prototype
https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/call
```javascript
Food.prototype = new Product();
```
