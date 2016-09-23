### 何謂module

ES5 (ECMAScript 5) 時，JavaScript本身並沒有內建module的概念. module一般可視做Function及資料(object)的集合.

third-party的各種module實作可參考下面 **大型前端專案的架構**的介紹. module實作常見方式:

1. 基本上用Object Literal Notation `var obj={}`就可以達到module化，包含member function, member property. 
2. 但是若想要使用/模擬private data/function, 則需要透過closure來達到.

#### 如何export module
待補充

### closure (特化的function跟scope)

**可提供類似其他語言的static function-使用static data, 以及跟module pattern結合提供內部private function的空間**

**closure使用到的變數的lifetime**只要還有人指到這個closure function時，這些變數就會隨著存活.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures*A closure is a function having access to the parent scope, even after the parent function has closed.*

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

### module pattern (通常是使用到匿名function)

套用closure在module pattern上時, 過程都會返回一個使用`{}`Object Literal Notation的object.

module相關-1:Mastering the Module Pattern[https://toddmotto.com/mastering-the-module-pattern/](https://toddmotto.com/mastering-the-module-pattern/)

module相關-2:大型前端專案的架構[https://medium.com/@benzwjian/%E5%A4%A7%E5%9E%8B%E5%89%8D%E7%AB%AF%E5%B0%88%E6%A1%88%E7%9A%84%E6%9E%B6%E6%A7%8B-cc235aacced0](https://medium.com/@benzwjian/%E5%A4%A7%E5%9E%8B%E5%89%8D%E7%AB%AF%E5%B0%88%E6%A1%88%E7%9A%84%E6%9E%B6%E6%A7%8B-cc235aacced0)

p.s.套用closure在module pattern上時, 過程都會返回一個使用`{}`Object Literal Notation的object. 但其實private method也可以發生在`new Object()`這內部. [http://stackoverflow.com/questions/1535631/static-variables-in-javascript](http://stackoverflow.com/questions/1535631/static-variables-in-javascript)以及下面ES6章節的link2都有提到.

### JavaScropt的event loop, thread
待補充

### timeout
~~~ javascript
setTimeout(function(){ console.log("timeout"); }, 3000);
~~~

### timer的用法跟陷阱
~~~ javascript
// closure problem
for(var i=0; i<10;i++){ 
  setInterval(function(){ 
    console.log(i); // 10, 10, ...., 10 !!! 
  }, 5000);
}

How to fix it ??
1. use ES6的blocked scope keywoard, let
2. use another function to forcely pass by value (i)
~~~