### 閉包closure (特化的function跟scope)

**其他語言也有closure**

**可提供類似其他語言的static function-使用static data, 以及跟module pattern結合提供內部private function的空間**

**Closure使用到的變數的lifetime**只要還有人指到這個closure function時，這些變數就會隨著存活.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures *A closure is a function having access to the parent scope, even after the parent function has closed.*

上述link有提到跟 closure相關的 **lexical scoping**:  

*the code and see that this works. This is an example of lexical scoping: in JavaScript, the scope of a variable is defined by its location within the source code (it is apparent lexically) and nested functions have access to variables declared in their outer scope.*

上述link裡的example, 放在online JB Bin上:[http://jsbin.com/wurihum/edit?html,js,output](http://jsbin.com/wurihum/edit?html,js,output) 其code:

~~~ javascript
var add = (function () {
  var counter = 0;
  debugger;  
  return function () {
    counter = counter +1;
    debugger; //用chrome dev tool看, 會看到closure scope
    return counter;  
  };
})();

add();
debugger;
add();
debugger;
add();
~~~
