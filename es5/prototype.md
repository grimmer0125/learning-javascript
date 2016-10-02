## [進階] JavaScript的 Prototype

**Prototype主要可以用來做/模擬傳統物件導向的繼承 inheritance**

參考:

1. Function.prototype
[https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/prototype](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/prototype)
2. [重要]Inheritance and the prototype chain, 使用 `Object.create`去建立一個新物件並且其prototype為傳進去的物件.
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain

~~~ javascript
var a = ["yo", "whadup", "?"];
// Arrays inherit from Array.prototype
// a ---> Array.prototype ---> Object.prototype ---> null

function f(){
  return 2;
}
// f ---> Function.prototype ---> Object.prototype ---> null

~~~

重點Notes:

1. `someobject.[[Prototype]]` 等價於 物件的`__proto__`(deprecated). 但`someobject.[[Prototype]]`跟`Function物件裡的.prototype`不一樣. 見上面**Inheritance and the prototype chain**的說明.
3. 不管是property或是method, access時若果當前type沒有找到此property/method, 都會往它的prototype指到的物件去找，遞迴的一直找到為止/或找到Object都沒有
4. 為什麼常見自訂object type的method要用`Car.prototype.autopilot`此寫法，是因為在new Car()時, 它會copy這個Car(<-一function object)的prototype到新建的prototype property.
5. 第4點補充: `var g = new Graph();` **`g.[[Prototype]]` is the value of `Graph.prototype` when new Graph() is executed.**
5. `Object.create`的概念

以下是各種不同使用`.prototype`來做繼承的examples. example-2 & example-3應該比較像是其他物件導向語言裡的繼承.

**example-1**: 使用 `Object.create(某物件)`;並且繼承的人可以改到obj的property. 但會需要注意如下case的情形.

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

**example-2**: 使用 `Object.create(某Function/type.prototype)`;

**2-i** 這篇有提到 多型polymorphism & factory pattern
http://stackoverflow.com/questions/34525517/angularjs-how-to-achieve-polymorphism-dependency-injection-best-practices
~~~ javascript

function Auto(name,year){
   this.year=year;
   this.name=name;
}
Auto.prototype.showYear = function(){
   console.log(this.year);
}
function Car(name,year, model){
   Auto.call(this,name,year);
   this.model=model;
}

 // Auto.prototype(給new物件時用)跟Auto自己的prototype property(__proto__)不一樣.
 // 且這兩個在這case裡都跟this.year, this.name沒關係.  
Car.prototype = Object.create(Auto.prototype);
~~~

**2-ii** 這篇有提到 多型polymorphism
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

**example-3**: 不使用`Object.create`, 直接指定某Function/Type其Prototype, `prototype = new Product()`做到類似`Object.create`繼承的效果
https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/call

~~~ javascript
function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}
Food.prototype = new Product(); // 注意這一行.
var cheese = new Food('feta', 5);
~~~
