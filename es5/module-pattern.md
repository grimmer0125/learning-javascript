### module pattern

**module相關-1:Mastering the Module **Pattern[https://toddmotto.com/mastering-the-module-pattern/](https://toddmotto.com/mastering-the-module-pattern/)

module pattern經常會與 closure+self invoke function一起使用,

~~~ javascript

var Module =
(function () {

 var x = "Hello!!"; // I will invoke myself

 return {
   name:"apple",
   test: function(){},
 }
})();

~~~

套用closure在module pattern上時, 過程都會返回一個使用`{}`Object Literal Notation的object.

**module相關-2:大型前端專案的架構**[https://medium.com/@benzwjian/%E5%A4%A7%E5%9E%8B%E5%89%8D%E7%AB%AF%E5%B0%88%E6%A1%88%E7%9A%84%E6%9E%B6%E6%A7%8B-cc235aacced0](https://medium.com/@benzwjian/%E5%A4%A7%E5%9E%8B%E5%89%8D%E7%AB%AF%E5%B0%88%E6%A1%88%E7%9A%84%E6%9E%B6%E6%A7%8B-cc235aacced0)

**整理:**
1. 基本上只使用Object Literal Notation `var obj={}`就可以達到module化，包含member function, member property.
2. 若一般module想要使用/模擬private data/function, 則需要透過closure來達到.

**closure與module**
透過closure來達到private data/function, 除了運用在常見的module pattern+self invoke function上面, 也可以發生在`自訂object`內部. 可參考
1.  [http://stackoverflow.com/questions/1535631/static-variables-in-javascript](http://stackoverflow.com/questions/1535631/static-variables-in-javascript)以及
2. 下面ES6章節的[link2](http://stackoverflow.com/questions/27849064/how-to-implement-private-method-in-es6-class-with-traceur)都有提到.
