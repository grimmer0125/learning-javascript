# JavaScript ES6 語法說明

**ES6 = ECMAScript 6 = ECMAScript 2015. **

ES6 還是未有直接support class的 private member當使用const/let等時, 且在node.js上, 則一定要運行在Strict Mode Code下, 即`use strict`. 不然會出現 Block-scoped declarations (let, const, function, class) not yet supported outside strict mode

ES6 如何在class上模擬private data/method:1. [http://www.2ality.com/2016/01/private-data-classes.html](http://www.2ality.com/2016/01/private-data-classes.html)2. [http://stackoverflow.com/questions/27849064/how-to-implement-private-method-in-es6-class-with-traceur](http://stackoverflow.com/questions/27849064/how-to-implement-private-method-in-es6-class-with-traceur)上述兩個link都提到兩種方式WeakMap & Symbol

### ES6 的 arrow function 會自動把當前的this傳進去, 等於隱性的使用`bind`.

**參考的連結:** [https://grimmer.io/javascript-notes/](https://grimmer.io/javascript-notes/)
