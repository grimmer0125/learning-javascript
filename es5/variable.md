## JavaScript 基本特性, 變數

### 直譯式語言的特性
* 沒先編譯. 一行一行逐行執行.
* 逐行直行時的特例: Function Hoisting, Function Declartion會被提升到當前scope的最頂端. 參考[JavaScript Function Definitions](http://www.w3schools.com/js/js_function_definition.asp)

### 除法

在`c`程式語言裡面, `2/3=0`, `3/2=1`. 在多數語言也是如此.

在`JavaScript`程式語言裡, `3/2=1.5`, 若要取整數部份則需要用到`Math.floor(3/2);//=1;`

### Exception & Crash & Assert

其他語言會crash但JavaScript不會的case:

1. `var test_array=[1,2]`, 其大小是`2`, 但access到超出範圍, e.g. `var k = test_array[100]`. 
2. 除以`0`

JavaScript exception常見case:使用到未宣告的物件

其他語言有的有兩種, 三種, JavaScript只有Exception

* Exception可以try-catch
* 可以自己製造Exception, 事先做一個如果真的發生時的提醒, 來debug.
* 通常發生Exception如果沒有catch住，程式也會掛掉，不過Browser如果是在本地端發生exception (比如說按一個button執行JavaScropt code時，下一次按button還是會去執行那段code.

### 記憶體管理

自動回收. 沒有人指到這物件就會被回收掉.

### JavaScript 裡的變數自動轉型

[https://msdn.microsoft.com/zh-tw/library/67defydd(v=vs.94).aspx](https://msdn.microsoft.com/zh-tw/library/67defydd(v=vs.94).aspx)

~~在 JavaScript 中，您可以針對不同型別的值執行運算，而不會發生例外狀況。  JavaScript 解譯器會將其中一種資料型別隱含轉換 (或「強制型轉」(Coerce)) 成其他資料型別，然後再執行運算。  字串、數字和布林值的強制型轉規則如下：  
如果您合併使用數字和字串，數字會強制型轉為字串。
如果您合併使用布林值和字串，布林值會強制型轉為字串。
如果您合併使用數字和布林值，布林值會強制型轉為數字。~~

### 變數的宣告跟定義

1. 其他語言function有時也有分宣告declaration 跟定義definition, 但JS主要是變數比較有在分.
2. 沒有宣告 跟沒有定義是不同的
    1. `var x; console.log("x:",x);` , print "undefined", no exception
    2. `console.log("y:",y);` , 沒有先宣告但直接使用時, exception如下,`exception: Uncaught ReferenceError: y is not defined`, 字有包含not defined但其實這case是連宣告也沒有.

### 變數的copy, 以及 Call by value vs Call by reference

變數基本上有兩種. 一種是純值的value type, 一種是object/function的reference.(事實上function本質上也是個物件[https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function))

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
