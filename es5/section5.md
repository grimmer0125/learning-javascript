## Function, Object, Scope, this  

### JavaScript裡的Function的基本介紹

#### 與Function相關的scope, this會在其他章節提到

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
`function test(x1,x2){
  console.log(arguments); // arguments={1:1,2:2,3:3}`
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
`var x = function (a, b) {return a * b}`
~~~
The function left is actually an **anonymous function** (a function without a name).

#### JavaScript中的Function definition: expression, declaration

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

詳細的差別: http://blogger.gtwang.org/2014/04/defining-javascript-functions.html

### Scope (變數存活的地方)
* 有三種. Global, Local (Function裡), Closure.
* 而Global全域變數其實就是全域物件(唯一)的屬性。瀏覽器：window物件、node.js：GLOBAL物件.
* 可開Chrome Dev tool 看變數的種類.

### Scope 對於變數的存取限制
在任何語言裡, 不同scope裡的變數若有名字一樣，則是以當前scope的最小scope裡的變數來使用. 外面層無法access到裡面的scope. 此事對於內部function的宣告以一樣.

~~~ javascript
var y= 3;
function test1(){
  var y = 100;
  console.log("y:",y); //100  
  var x =5;  
  function test2(){
    var y = 0;  
  }
}
test1();
console.log(x); // exception
test2(); //exception too
~~~

反而過, `In fact, in JavaScript, all functions have access to the scope "above" them.`[http://www.w3schools.com/js/js_function_closures.asp](http://www.w3schools.com/js/js_function_closures.asp)

### Functional Scope (即Local scope) 的注意事項-1
~~~ javascript
if(true){
  var x = 3;
}

// 在其他某些語言裡, scope是block的, 即離開了{}變數會不存在.
// 但JavaScript是Functoinal scope的. Python也是
console.log("x:",x); //x:3
~~~

### JavaScript Object的建立

有以下3方法, 參考[http://www.w3schools.com/js/js_object_definition.asp](http://www.w3schools.com/js/js_object_definition.asp)

1. Object Literal Notation.
~~~ javascript
var car = {name:"BMW", autoDrive:function(){}};.
~~~
較難重複製造並使用建立的屬性, 常用來用在屬性欄位不固定的case.
2. 自建物件類型(type, 有自己的名字). 使用`new` keyword.
~~~ javascript
    function Car(){
      this.name="";
      this.setName=function(){
      };
    }
~~~
接著使用`var car1 = new Car();`方便重複使用. 較為接近一般語言裡的物件化的方法.

3. 這方法較少用, 較難重複製造並使用建立的屬性.

~~~ javascript
var person = new Object();
person.firstName = "John";
~~~

### JavaScript的Object Literal Notation

JavaScript Object用的Object Literal Notation方法可以做為module的一種方式(做為module的方式時通常會放functions在內部當做其property), 可以在某些時候export給別人用.

~~~ javascript
var myModule = {
  myProperty: 'someValue',
  //object literals can contain properties and methods.
  //here, another object is defined for configuration purposes.
  myConfig: {
    useCaching: true,
    language: 'en'
  },

  // a very basic method
  myMethod: function() {
    console.log('I can haz functionality?');  

    //可以用 this 來存取其他的property  
    console.log('this.myProperty:', this.myProperty);
  }
}

console.log(myModule.myConfig);
myModule.myMethod();
~~~

### this (其他語言通常是在物件內部存取自己時使用this/self等keyword)

可參考別人整理的很好的 **JavaScript：this用法整理**: [https://software.intel.com/zh-cn/blogs/2013/10/09/javascript-this](https://software.intel.com/zh-cn/blogs/2013/10/09/javascript-this), 摘要

1. 有一句話可以形容`this`:**Javascript裡的this看的是究竟是誰調用該函式**
2. 它裡面提到的當是在Node.js情況下, *故輸出應為`undefined`* 應改為 `{}`, 進一步的解說是:  

Node.js 一般使用時 (node index.js)，檔案的最外層並不是global scope(意指會利用function將code整個包起來執行). 在最外層下一開始`this={}`, 要access global要用`global`這個關鍵字當做keyword來存取global物件，但一進去任何function裡，它的this就會變成指到global了。

**this的重點:**
1. `this`是指到現在這位置的(物件)owner. Local scope下都有個`this`來指向某物件.
2. 當產生物件時, 即`new` or `.` or 'var car ={}', 在進去其functions時, `this`會切換成物件的參考reference.
3. 當直接呼叫function時(沒有使用. or new or ={} or bin/call/apply時)，`this`都是指向global scope的唯一物件(browser:window, node.js:global)
4. 術語`context`就是等於 *this指到/參考到的物件*

### Scope, this 的例子-1 (變數宣告的各種case)

一般在browser上執行時. 變數的分類有

1. 成為object的property
2. local變數 (如果是在browser最上層就變成打`var x=3`則會自動變成global object的property)

使用上除了直接指定為object的property外, e.g. `obj.x=3`, 有其他幾種宣告方式

1. `var x = 3;`.
2. `x = 3;//前面沒有打var/let/const`, 在Local scope這樣使用時, 若已有同樣名字的當然就是直接使用其Local變數. 若沒有, 則會變成global物件的屬性(宣告直接使用).
3. `this.x = 3;`

下面是此為function的物件化時的case.

~~~ javascript

// test in chrome console
// var y等於y等於this.y 在browser最上層
var y = 300;
y = 400;

console.log("this.y:", this.y); // 400
console.log("y:", y); // 400 !!!
console.log("this:", this); // will print many things

function TodoView() {

  // Local:
  //       x:      // 200
  //       this:  
  //            x  // 100

  this.x = 100;  
  var x = 200;

  console.log("this.x in TodoView:", this.x); // 100
  console.log("x in TodoView:", x); //200
}

var xx = new TodoView();

~~~

如果上面最後是 `TodoView();` 非物件時, 結果會不一樣.

### Scope, this 的例子-2, callback時的bind

以下是沒有使用`bind`的case, 線上JS Bin的example code[https://jsbin.com/tunamas/edit?html,js,console,output](https://jsbin.com/tunamas/edit?html,js,console,output)

~~~ javascript
// app.js
function TodoView() {

  this.x = 100;

  this.clickBtnListner = function() {
    console.log("x:", this.x); // undefined, not exception !!  
  }

  var button = document.getElementById("clickbutton");
  button.addEventListener('click', this.clickBtnListner);
}

app = new TodoView();

// index.html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
</head>
<body>
  <button id="clickbutton">Click Me!</button>
    Try it Yourself
  <script src="app.js"></script>
</body>
</html>

~~~

使用`bind`解決此 exception: **x is not defined**
~~~ javascript
$("button-click").addEventListener('click', this.clickBtnListner);
~~~
改成
~~~ javascript
$("button-click").addEventListener('click', this.clickBtnListner.bind(this));
~~~

### callback時的 call, apply

跟`bind`類似的還有 `call`, `apply`, 上述某section有提到的[https://software.intel.com/zh-cn/blogs/2013/10/09/javascript-this](https://software.intel.com/zh-cn/blogs/2013/10/09/javascript-this) 也有提到'call','apply'. 可參考, 不過它的case 5.例子沒有清楚.

可另外參考[http://dreamerslab.com/blog/tw/javascript-call-and-apply/](http://dreamerslab.com/blog/tw/javascript-call-and-apply/), 這網頁裡使用 `call`, `apply`在設計callback.

### callback的bind, call, apply使用時機整理
**1. 不需使用的case**
一種常見的是API的callback只有設計回傳值, 當然就沒有`this`等這些困擾

**2. 設計者處理:**

如果是像[http://dreamerslab.com/blog/tw/javascript-call-and-apply/](http://dreamerslab.com/blog/tw/javascript-call-and-apply/)的, 自己設計一個object中的註冊callback function的API, 且callback function中要可以access同一object的mebmer, 實作時可用`apply`, `call`.

**example** (進階,可看可不看)

此 example 出現兩個callback, 一個自己實做, 一個jQuery

~~~ javascript
function Album(title){
  this.name = title;
  this.data;
}
var album = new Album('Taiwan');

// 實作 getFromName的使用callback流程, 使用call or apply
Album.prototype.getFromName = function( callback ){
  var self = this;  

  $.get( '/albums/' + this.name , function( data ){
    callback && callback.call( self, data );
  });
};

// 使用時, 這裡的this就是album本身
album.getFromName( function( data ){

 //因為要access this.name(album的name) 所以上面實作時要用call or apply.
  alert( 'The album' + this.name );
});
~~~

jQuery API case都是上述這種設計方式. [https://api.jquery.com/click/](https://api.jquery.com/click/), 線上code:

[https://jsbin.com/tunamas/edit?html,js,console,output](https://jsbin.com/tunamas/edit?html,js,console,output)

~~~ javascript
$('.jQueryButton').click(function(){
  console.log("click jquery button");
  var $this = $(this); //this對應到$('.jQueryButton')得到的button物件
  $this.text('Clicked');
});
~~~

**3. 使用者處理:**

若是像是上述`bind`的case, this.x的this(指的是TodoView物件)跟button不是同一物件, 則需要的是`bind`.即使用這callback的人自己去加.
~~~ javascript  
button.addEventListener('click', 這邊傳入的callback最後會用到this.x);
~~~

**若同時使用 `call`, `bind`, 則以`bind`傳進去的為主.**

### 常見技巧:使用self. 目的是在不同的scope(function)裡存取外部的物件, 自定一個稱呼為 self 的變數.

**這裡的技巧本質上是跟closure有關**

在其他語言裡, 在不同function要存取不在function裡定義的物件, 通常是直接把物件當作參數傳進去. JavaScript也很常見.e.g.
~~~ javascript
function changeObj(refObj){
  // refObj.name = "abc";
}
var obj = {name:""};
changeObj(obj);

// 甚至也可以把 this 丟進去, 因為this一定是指到某物件
changeObj(this);
~~~

但因為JavaScript裡常出現function裡面有function (nested function), 所以另一個做法是：

~~~ javascript
function test1(){

  // 此時this是新的test1物件.  
  // 如果是直接在外面執行 test1();則this是global物件.
  var self = this;   
  test2();  

  function test2(obj){
    // 此時這裡的this指到的是global物件.  
    // 若要存取上面的test1物件, 可以
    // 方法1.把上面改成test2(this), 把this傳進來  
    // 方法2 直接使用self (其實就是closure應用)  
  }
}

new test1();
~~~
