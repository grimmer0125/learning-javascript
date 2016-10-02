### 何謂module

ES5 (ECMAScript 5) 時，JavaScript本身並沒有內建module的概念. module一般可視做Function及資料(object)的集合. 且通常是散布在多個檔案裡.

### 一個Project中使用多個JavaScript檔案
通常是
1. 自己的一個JS檔案 + 引入別人寫好的JS檔案
2. 自己的就拆成多個檔案, 這樣可以避免一個檔案過大

**在Browser端:**
可由`<script>`來引入JS檔案, 下面的例子中, B.js因為是後引入的, 所以可以讀到A.js裡的global變數, 且B.js定義的global function會蓋過A.js同名字的，就等同於兩個JS檔案拼在一起.
~~~ javascript
    <script src="A.js"></script>
    <script src="B.js"></script>
~~~

**在Node.js端:**
需使用Node.js自己實作的[CommonJS module](https://nodejs.org/docs/latest/api/modules.html)方式(`require/export`)

third-party的各種module實作細節可參考下面 **大型前端專案的架構**的介紹.

#### 如何export module
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
