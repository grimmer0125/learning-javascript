## ES5的自訂物件類型 - 使用 prototype

### 非自建物件類型的, 即`var obj ={};`, 可參考上一個章節的Object Literal Notation

### ES5, 自建物件類型的method宣告方式 以及static method/data:

物件的member成員若是function, 通常叫做method.

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
