# JavaScript ES5 基本語法說明

### Debugger工具

* console.log("error:", json); console.log("msg:"+"string"); console.log("err:%s", message);
* 可以安裝 [https://code.visualstudio.com/](https://code.visualstudio.com/)方便用Node.js設定中斷點debug. 
* 在browser的環境下，也可以用 [Window alert](http://www.w3schools.com/jsref/met_win_alert.asp)來直接跳出警告訊息來debug.

### pseudocode 虛擬碼

[https://zh.wikipedia.org/wiki/%E4%BC%AA%E4%BB%A3%E7%A0%81](https://zh.wikipedia.org/wiki/%E4%BC%AA%E4%BB%A3%E7%A0%81)虛擬碼（英語：pseudocode），又稱為偽代碼，是高層次描述演算法的一種方法。它不是一種現實存在的程式語言（已經出現了類似虛擬碼的語言，參見Nuva）；它可能綜合使用多種程式語言的語法、保留字，甚至會用到自然語言。它以程式語言的書寫形式指明演算法的職能。相比於程式語言（例如Java、C++、C、Delphi 等等）它更類似自然語言。它是半形式化、不標準的語言。我們可以將整個演算法執行過程的結構用接近自然語言的形式（這裡可以使用任何一種作者熟悉的文字，例如中文、英文，重點是將程式的意思表達出來）描述出來。使用虛擬碼，可以幫助我們更好的表述演算法，不用拘泥於具體的實作。

e.g. `迴圈跑個五次`

### Coding style and naming convention

* 縮排跟coding style很重要, `var x = 5`; 比`var x =5`好. coding style可參考airbnb的, [https://github.com/airbnb/javascript](https://github.com/airbnb/javascript). 縮排又可以分為使用`soft tab`(spaces,建議用這個)跟`Tab characters`.
* naming convention命名很重要, 請參考[http://www.w3schools.com/js/js_conventions.asp](http://www.w3schools.com/js/js_conventions.asp)

### Atom的一些tips

* `cmd+left` 跳到當行最前面, `cmd+right` 跳到當行最右邊. 
* 用游標選取一段文字, `cmd+/` 可以把整段文字變成註解.
* 用遊標選取一段文字, `cmd+[`以及`cmd+]` 可以把向左或向右移一個tab縮排. 
* atom可以使用 [jsformat](https://atom.io/packages/jsformat) 來自動排版(使用基本通用的規則)，若需要更進一步符合特定coding style, 可使用[`linter-eslint`](https://atom.io/packages/linter-eslint) 來套用airbnb的coding style package, 安裝方式待補充, 這些類似可能需要擇一安裝，因為通常會有save時自動修正的功能，會衝突.

### Online 測試JavaScript code的方法
1. Chrome的console(有部份自動完成), 多行輸入:`shift+enter`. ref: [https://coderwall.com/p/bv0k0q/enter-multiple-lines-in-chrome-js-console](https://coderwall.com/p/bv0k0q/enter-multiple-lines-in-chrome-js-console)
2. 其他網站提供的, 單人方便練習html+js+css的工具, 無法多人同時edit, 但都可選es6, 且引入外部lib:  e.g. [https://jsbin.com](https://jsbin.com)<-有自動完成 or [http://codepen.io/](http://codepen.io/)

### snippet

Chrome的snippet不僅可以存code的片段, 也可以用來測試[https://developers.google.com/web/tools/chrome-devtools/debug/snippets/](https://developers.google.com/web/tools/chrome-devtools/debug/snippets)

線上snippet: [https://gist.github.com/](https://gist.github.com/)

本機snippet/markdown:[boostnote](https://b00st.io/)

### 直譯式語言的特性
* 沒先編譯. 一行一行逐行執行. 
* 逐行直行時的特例: Function Hoisting, 參考[JavaScript Function Definitions](http://www.w3schools.com/js/js_function_definition.asp) 

### 除法

在`c`程式語言裡面, `2/3=0`, `3/2=1`. 在多數語言也是如此.

在`JavaScript`程式語言裡, `3/2=1.5`, 若要取整數部份則需要用到`Math.floor(3/2);//=1;`

### 變數的宣告跟定義

1. 其他語言function有時也有分宣告declaration 跟定義definition, 但JS主要是變數比較有在分. 
2. 沒有宣告 跟沒有定義是不同的 
    1. `var x; console.log("x:",x);` , print "undefined", no exception 
    2. `console.log("y:",y);` , 沒有先宣告但直接使用時, exception如下,`exception: Uncaught ReferenceError: y is not defined`, 字有包含not defined但其實這case是連宣告也沒有.

### 變數的copy, 以及 Call by value vs Call by reference

變數基本上有兩種. 一種是純值的value type, 一種是object/function的reference.

一個function傳進去的變數叫做argument, function宣告及在內部使用的叫做parameter, 例子: [http://stackoverflow.com/questions/1788923/parameter-vs-argument](http://stackoverflow.com/questions/1788923/parameter-vs-argument).

呼叫一個function時傳進去的變數跟function paramter的關係其實就是 **copy變數**: `var x= something; var y=x` 一樣. 以下例子.

~~~ javascript
// copy value
var x = 5; 
var y = x; 
y = x;
y = 6; 
console.log("x:", x); // 5
console.log("y:", y); // 6

// copy reference: 
var x = {name:"google"}; 
var y = x;
y.name = "tesla";
console.log("x:", x); // name: "tesla"
console.log("y:", y); // name: "tesla"

// call by reference
function testChange(z){ 
  z.name = "microsoft";
}

testChange(x);
console.log("x:", x); // name: "microsoft"
~~~

### 物件變數傳進去function裡的注意事項
~~~ javascript 
function test1(obj){

  // 等於右邊建了個新的物件, 指給obj. 不管原本testObj是什麼值(就算不是null),  
  // 之後obj也都不會改變到testObj  
  obj = {name:"123"};
}

// 常見的assign(等於copy等於"=")整個物件變數的方法之一
function test2(obj){

  // obj = null, outside testObj = null;  
  obj = {name:"123"}; 
  return obj; 
}

var testObj = null; 
test1(testObj); 
console.log(testObj); // still null

testObj = test2(); //不傳參數進去沒關係, JS的function可以接受參數個數不match. 
console.log(testObj); // {name:"123"};

~~~

### 常見的改變物件變數其property的方法
~~~ javascript
function test2(obj){
  obj.name = "abc"
}
var testObj = {}; //若是null, 傳進去裡面執行obj.name會有exception
test2(testObj);
console.log(testObj); // {name:"abc"}

~~~

### 字串 String

為JavaScript內建基本型別(primitive type)之一(C裡面沒有, C內建是char),` `` ` 跟 "" 都可以用來表示字串. 且JS裡字串為`value type`.

#### substring
http://www.w3schools.com/jsref/jsref_substring.asp
~~~ javascript
var str = "Hello world!";
var res = str.substring(1, 4); //(start, end), not includes end
// output: ell
~~~

### 變數檢查, ==, ===, typeof 檢查型別

`===` 這個operator 會同時會比較值跟type, `==` 只會比較值而已.

常見的初始值有下面幾種, 以下幾種的`===`都各不相等

1. `0`
2. `false`
3. `"0"`
4. `""` , `這前4個用 == 大部份都是true, 只有3&4的==不會等於true`
5. `null` ,`var x= null;常用來表示x是reference type但還未得到值` 
6. `undefined` ,` var x;`, 宣告但沒有定義
7. `[]`
8. `{}`

~~~ javascript
// empty array case
var a =[];
var b =0;
if(a==b){
  //will hit here
}
~~~

**檢查是那一種type**
~~~ javascript
var d = "test"; 
console.log(typeof d); //string
if (typeof d == "string"){
  //will hit here
}

// 可用下面方法來run有值時的logic. 有時沒值是因為還留在初始化的狀態. 
if(x){ 
  // 可以用這方式來檢查是否為 0,false,"0","",null, undefind, 
  // 都不是才會進來.
}

// 但有個特殊case, 如果x這個變數沒有宣告過, 直接用會exception.可用下面方法

if (typeof x != 'undefined'){ 
  //如果只是未宣告, 則一定不會進來這邊. 
}
~~~

### Callback function

為各式各樣的 **API(e.g.jQuery)** 或`EventListener` 的基礎

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

callback有分需要用到this, 以及沒有需要用到this的case.即上述兩例, 後面的sections會詳細講解this.

### Array的操作

JavaScript的Array是non typed的，即每個成員可以type不一樣，跟Object一樣.

~~~ javascript
var list = [1,"2", [1,2,3]] 
~~~

### Array裡的單一元素操作, 其取出copy到另一變數時遵照一般的規則

~~~ javascript
var array = [{name:"apple"}, "map", "mop"];
var secondElement = array[1]; //copy of value type 
secondElement = "abc"; 
console.log(array); // [{name:"apple"}, "map", "mop"]; same

var firstElement = array[1]; //copy of reference type
first.name = "abc"; 
console.log(array); // [{name:"abc"}, "map", "mop"]; change
~~~

#### Array的copy (array本身是reference type)

array2等於array1, 透過array2改, 印出array1也被改到

~~~ javascript
// Array is reference case
var list1 = [1, 2, 3];
var list2 = list1; //把list1 assign給list2
list1[0] = 4;
console.log("list1:", list1); // [4, 2, 3]
console.log("list2:", list2); // [4, 2, 3]
~~~
#### Array的deep copy/clone/duplicate (copy each element)

**使用 `slice()` **[http://www.w3schools.com/jsref/jsref_slice_array.asp](http://www.w3schools.com/jsref/jsref_slice_array.asp)
~~~ javascript

// case 1, element為純type類型
var oldArray = ["mip", "map", "mop"];
var newArray = oldArray.slice();
newArray[1]="123"; // "mip", "123", "mop"
//oldArray keeps the same, "mip", "map", "mop"

case 2, element有JSON object, 即結合Array跟JSON的複合型態, 新的array可以改到舊的array的key/value嗎? yes.

var oldArray = [{name:"apple"}, "map", "mop"];
var newArray = oldArray.slice();
newArray[0].name = "google"; //第一個element為物件類型. 
//oldArray: [{name:"google"}, "map", "mop"], is google !!!

由以上兩個cases可看出, slice()產生新的array內部是對單一element的copy, follow value/reference的rule.    

~~~

`slice()`另一用途: 用來取某一部份的array的值, e.g. `slice(1,3)`, 從1取到2.

#### Array的 For-Loop 
有兩種
1. Iterator, e.g. `for student of students`
2. `for (var i=0; i< 100; i++)`

ES6才有array的`for-of` [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of), 

ES5的array要用 `int i = 0`的方法.

### 遞迴(Recursion)

**算是除了loop/iterationg以外另一種實現方式.**

1. 可練習
2. 在很多語言裡是比較慢的. 有些語言可能較快. 可參考 [http://stackoverflow.com/questions/2651112/is-recursion-ever-faster-than-looping](http://stackoverflow.com/questions/2651112/is-recursion-ever-faster-than-looping)
3. JavaScript的遞迴跟大多數一樣, 是比loop慢的, http://stackoverflow.com/questions/9474465/is-iteration-faster-than-recursion-or-just-less-prone-to-stack-overflows

### Array的high order function操作map, filter, reduce

**建議若可以用這些語言內建的function, 盡量用, 因為本身通常都有優化過, 較快.** 參考上面的Link [http://stackoverflow.com/questions/2651112/is-recursion-ever-faster-than-looping](http://stackoverflow.com/questions/2651112/is-recursion-ever-faster-than-looping)

map(很常見): 對每一個元素做處理, 形成新array. [https://msdn.microsoft.com/zh-tw/library/ff679976(v=vs.94).aspx](https://msdn.microsoft.com/zh-tw/library/ff679976(v=vs.94).aspx)

e.g.
~~~ javascript 
var newList = [1, 2, 3].map(function(x) { 
  return x + 1;
}) // [2, 3, 4]
~~~

filter: 對每一個元素做篩選, 形成新array [https://msdn.microsoft.com/zh-tw/library/ff679973(v=vs.94).aspx](https://msdn.microsoft.com/zh-tw/library/ff679973(v=vs.94).aspx)

reducer: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
*The reduce() method applies a function against an accumulator and each value of the array (from left-to-right) to reduce it to a single value.*

### JSON的注意事項及常見處理

JSON (JavaScript Object Notation)為從JavaScript Object推廣而來的一種資料格式，JSON本身是代表JavaScript物件的標記方法，而JavaScript Object的簡化型 (無function，純value type) 就是對應到此種資料格式，故JSON同時有兩種意思。JSON在其他語言可能名字是Map/KeyValue/Dictionary. 跟Array一樣為兩大常見的資料形態.

~~~ javascript
var data = { 
  name: "apple", //key也可以為"name"有引號的形式 
  size: 1000 
}
~~~

1. 如何access其property對應到的值或物件: 

    1. `data.name` 
    2. `data["name"]` 
    3. `var key="name"; data[key];`

2. 如何事先檢查property有無存在 (通常會在上述第1點前檢查), 如果不檢查則  `var nameValue = data.name; //undefined`,事後用可能exception或logic不符合 

    1. `if(data.name){}`, 如果物件沒有name這個property, 不會進去.  
    2. `data.hasOwnProperty(name)`,[https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty). 此方法在效能上比1.好，[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)這裡說 *hasOwnProperty is the only thing in JavaScript which deals with properties and does not traverse the prototype chain.*

3. `for-in`, [https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/for...in](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/for...in)
 找出一個一個key, 然後就可以obj[key]列出每一個value做處理.

4. `Object.keys(data)`. 把全部key都存成一個array. [https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/keys](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)

5. deepCopy每對key/value到新object. 使用 `Object.assign` [https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/assign](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

### 常見case - Loop Array 或 JSON/Map/Dictionary 時要小心的事情

有一個常見的use case是: 一個Array要挑出某個特定的element, 然後把它從這array裡移除掉. How?

### Exception & Crash & Assert

常見case1: `test_array`大小是`2`, 但access到超出範圍, e.g. `test_array[100]`, 通常會發生Exception/Crash

常見case2:使用到未宣告的物件

常見case3:除以`0`

其他語言有的有兩種, 三種, JavaScript只有Exception

* Exception可以try-catch
* 可以自己製造Exception, 事先做一個如果真的發生時的提醒, 來debug. 
* 通常發生Exception如果沒有catch住，程式也會掛掉，不過Browser如果是在本地端發生exception (比如說按一個button執行JavaScropt code時，下一次按button還是會去執行那段code.

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

### Functional Scope (即Local scope)
~~~ javascript
if(true){ 
  var x = 3; 
}

// 在其他某些語言裡, scope是block的, 即離開了{}變數會不存在. 
// 但JavaScript是Functoinal scope的. Python也是console.log("x:",x); //x:3
~~~

### Function
1. function一般有兩種.  
    1. 語言內建 
    2. 自己寫的或是別人寫好的. 但因為JavaScript的執行環境(平台)比其他語言還要來得多種. 所以Browser跟Node.js都各有提供它們平台上面非語言內建的function，且有些相容，有些不相容. 
2. function的arguments, 除了明顯的宣告parameters外，可以在function內部用arguments[i]的方式得到每一個argument, e.g. `function test(x1,x2){console.log(arguments)}; test(1,2,3);// arguments={1:1,2:2,3:3}` 
3. function裡面也可以有內部的function. 此特性在其他語言或多或少也有.
4. function也可以是一種object的定義 (透過`new`). JavaScript特有的觀念. ES6才有其他語言的class關鍵字. 
5. JavaScript Function Definitions [http://www.w3schools.com/js/js_function_definition.asp](http://www.w3schools.com/js/js_function_definition.asp) 
6. `var x = function (a, b) {return a * b}`; The function left is actually an **anonymous function** (a function without a name).

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

### JavaScript Objects的建立

有以下3方法, 參考[http://www.w3schools.com/js/js_object_definition.asp](http://www.w3schools.com/js/js_object_definition.asp)

1. Object Literal Notation. `var car = {name:"BMW", autoDrive:function(){}};`. 較難重複製造並使用建立的屬性, 常用來用在屬性欄位不固定的case.
2. 自建物件type(有自己的名字). 使用`new` keyword. Define `function Car(this.name="", this.setName=function{}){};`, 接著使用`var car1 = new Car();`方便重複使用. 較為接近一般語言裡的物件化的方法. 
3. `var person = new Object(); person.firstName = "John";`較難重複製造並使用建立的屬性

### this (其他語言通常是在物件內部存取自己時使用this/self等keyword)

1. `this`是指到現在這位置的(物件)owner. Local scope下都有個`this`來指向某物件.
2. 當產生物件時, 即`new` or `.` or 'var car ={}', 在進去其functions時, `this`會切換成物件的參考reference. 
3. 當直接呼叫function時(沒有使用. or new or ={} or bin/call/apply時)，`this`都是指向global scope的唯一物件(browser:window, node.js:global)
4. JavaScript：this用法整理. [https://software.intel.com/zh-cn/blogs/2013/10/09/javascript-this](https://software.intel.com/zh-cn/blogs/2013/10/09/javascript-this) <-超重要, 不過它裡面提到的*故輸出應為`undefined`* 應改為 `{}`, 在*Scope, this 的例子-2, bind*這一section會再提到. 
5. Node.js 一般使用時 (node index.js)，檔案的最外層並不是global scope(意指會利用function將code整個包起來執行). 在最外層下一開始`this={}`, 要access global要用`global`這個關鍵字當做keyword來存取global物件，但一進去任何function裡，它的this就會變成指到global了。
6. 術語`context`就是等於 *this指到/參考到的物件* 

有一句話可以形容`this':**Javascript裡的this看的是究竟是誰調用該函式**

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

### self invoke function (定義跟執行同時)

~~~ javascript
(function () { 
  var x = "Hello!!"; // I will invoke myself
})();
~~~

### 再講JavaScript的Object Literal Notation

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

### 記憶體管理

自動回收. 沒有人指到這物件就會被回收掉.

### JavaScript重點以及跟其他語言差異處

1. `this`的觀念, 及使用`bind`來改變this指向的object. 是其它語言比較沒有的.
2. 當直接呼叫function時(沒有使用`.` or `new` or `={}` or `bind/call/apply`時)，`this`是指到global物件. 
3. 可使用object literal notion, `{}` 來當做基本類型`JavaScript Object`的定義. 若{}沒有包含function, 就變成一般的JSON資料了.
4. global scope對應到一個global object.
5. function內部包含function宣告, 其他語言可能有類似但沒有這麼直接. 
6. object可runtime執行時輕易動態擴充member (ES5 way)
7. 多了 `===` 這個operator
8. 沒有`private`關鍵字
9. JavaScript沒有`C` type的pointer跟`C#/Java` 其reference的id.
