## 何謂module

ES5 (ECMAScript 5) 時，JavaScript本身並沒有內建module的概念. module一般可視做Function及資料(object)的集合. 且通常是散布在多個檔案裡.

### 一個Project中使用多個JavaScript檔案
通常是
1. 自己的一個JS檔案 + 引入別人寫好的JS檔案
2. 自己的就拆成多個檔案, 這樣可以避免一個檔案過大

**Browser端:**
可由`<script>`來引入JS檔案, 下面的例子中, B.js因為是後引入的, 所以可以讀到A.js裡的global變數, 且B.js定義的global function會蓋過A.js同名字的，就等同於兩個JS檔案拼在一起.
~~~ javascript
    <script src="A.js"></script>
    <script src="B.js"></script>
~~~

**Node.js端:**
需使用Node.js自己實作的[CommonJS module](https://nodejs.org/docs/latest/api/modules.html)方式(`require/exports`)

examples:
待補充

**Browser端可以使用像是webpack等打包JS工具**

[webpack](https://webpack.github.io/)有幾種功能

1. 把多個JS檔案合成一個, 這樣`<script>`使用一個就好
2. 同時把JS檔案minified混淆打亂過, 使別人無法輕易看到完整source code
3. 可使用Node.js的CommonJS的寫法(require等)來讓A file引用B file的東西.

**ES6的module (import/export)**

不管是Browser端以及Node.js端, 都沒有內建支援ES6的原生module語法.
但可以使用[Babel](https://babeljs.io/)等JS compiler工具來使用

語法參考:

[https://github.com/lukehoban/es6features/blob/master/README.md#modules](https://github.com/lukehoban/es6features/blob/master/README.md#modules)

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
