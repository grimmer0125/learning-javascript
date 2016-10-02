## JavaScript裡的Function的基本介紹

**與Function相關的new object, scope, this 會在[Object, Scope, this](es5/this.md)** 裡詳細介紹

可參考 JavaScript Function Definitions [http://www.w3schools.com/js/js_function_definition.asp](http://www.w3schools.com/js/js_function_definition.asp)

所謂的function/library一般有兩種.  

1. 語言內建
2. 自己寫的或是別人寫好的. 但因為JavaScript的執行環境(平台)比其他語言還要來得多種. 所以Browser跟Node.js都各有提供它們平台上面非語言內建的function，且有些相容，有些不相容.

function裡面也可以有內部的function(nested function). 此特性在其他語言或多或少也有, 但不像JavaScript那麼直接.

~~~ javascript
function test1(){
  function test2(){

  }
}
~~~

JavaScript裡, function本身除了是純function外, 也可以是一種object的定義, 並使用`new`來產生物件, 即此function同時像是 其他語言的constructer建構子一樣. ES6才有其他語言有的class以及正式的constructer function出現.

~~~ javascript
function test (){
  this.x = 100;
  return 0;
}
var test(); // use as function
var obj = new test(); //use as a constructer

~~~

#### function的arguments

function的arguments, 除了明顯的宣告parameters外，可以在function內部用arguments[i]的方式得到每一個argument, e.g.

~~~ javascript
function test(x1,x2){
  console.log(arguments); // arguments={1:1,2:2,3:3}
}
test(1,2,3);
~~~

亦也可以傳入少於定義的參數個數. 即
~~~ javascript
function test(x,y){
  // y will be undefined, (有宣告但無定義)
}
test(1);
~~~

#### anonymous function 匿名函數

~~~ javascript
var x = function (a, b) {return a * b}
~~~

The function left is actually an **anonymous function** (a function without a name).

#### JavaScript中的Function definition: expression, declaration

可參考: http://blogger.gtwang.org/2014/04/defining-javascript-functions.html

Expressoin:
~~~ javascript
var x = function(){
}
~~~

Declaration:
~~~ javascript
function test(){
}
~~~

Notes:

1. 如果是使用Exression的方式在loop裡, 會產生多次的Function Object.
2. Exression的使用要看當時的使用情境, 不過若使用則建議不採用匿名方式來幫助debug. [http://programmers.stackexchange.com/questions/160732/function-declaration-as-var-instead-of-function](http://programmers.stackexchange.com/questions/160732/function-declaration-as-var-instead-of-function), 即

~~~ javascript
var x = MY_function() {};
~~~

## Callback function

**[Object, Scope, this](es5/this.md)章節有一些進階的callback的例子, Array的map等function其實也有用到callback function**

在各種程式語言裡, callback function是很重要的概念. 應為各式各樣的 **API(e.g.jQuery)** 或`EventListener` 的基礎

通常可分為兩種角色

1. 定義 API/Callback介面的人(設計者)
2. 使用這 API的人(使用者), 需定義/實作callback function

~~~ javascript
//通常這個function會做
// 1. 一些動作： 比如說發http request,
// 或找本地端的html元件. 完成後把參數(e.g.網路資料/元件)傳給callback
// 2. 註冊callback function
function apiCall(callback_fun){   
// 做了一堆事情後, 可能有變數x, y, z
  var x=5, y=6, z =7;  
  callback_fun(x,y,z);
}

// 使用者用來讓別人call的function, 用來定義使用者想要怎麼處理資料的function
// 變數名稱沒有限制, 因為都是由設計者傳參數進去, 換言之也有可能不小心定義成3個,
// 但設計API的人只有傳2個, 要看文件
function printlog(x2,y2,z2){  
  console.log("hello");   
  console.log("x:",x2,";y2:",y2,";z2:",z2);
}

apiCall(printlog);
~~~

jQuery的例子:

~~~ javascript
$('.jQueryButton').click(function(){
  console.log("click jquery button");
  var $this = $(this);
  $this.text('Clicked');
});
~~~

**callback有分需要用到this, 以及沒有需要用到this的case.即上述兩例, 後面的sections會詳細講解this.**
