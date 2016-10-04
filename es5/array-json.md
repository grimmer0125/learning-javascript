## Array及JSON的操作

### Array的操作

JavaScript的Array是non typed的，即每個成員可以type不一樣，跟Object一樣.

~~~ javascript
var list = [1,"2", [1,2,3]];
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

#### 移除第一個元素以及最後一個元素

~~~ javascript
// remove the fist one, using shift
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.shift(); //the length becomes 3

// remove the final one, using pop
fruits.pop(); //the length becomes 2
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

// case 2, element有JSON object, 即結合Array跟JSON的複合型態, 新的array可以改到舊的array的key/value嗎? yes.

var oldArray = [{name:"apple"}, "map", "mop"];
var newArray = oldArray.slice();
newArray[0].name = "google"; //第一個element為物件類型.
//oldArray: [{name:"google"}, "map", "mop"], is google !!!

由以上兩個cases可看出, slice()產生新的array內部是對單一element的copy, follow value/reference的rule.    

~~~

**`slice()`另一用途: 用來取某一部份的array的值, e.g. `slice(1,3)`, 從1取到2.**

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

    1. `if(data.name){}`如果物件沒有name這個property, 不會進去. 會連它的prototype都查, 若要知道prototype, 請詳閱[ES5中的自訂物件類型-prototype](prototype.md)一章,  
    2. `data.hasOwnProperty(name)`, 介紹:[https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty). 而根據 [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) *hasOwnProperty is the only thing in JavaScript which deals with properties and does not traverse the prototype chain.* 此方法不會查prototype chain, 所以在效能上比1.好，關於JavaScript的prototype可參考**[進階-再講prototype](prototype.md)一章** 

3. `for-in`, [https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/for...in](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/for...in)
 找出一個一個key, 然後就可以obj[key]列出每一個value做處理.

4. `Object.keys(data)`. 把全部key都存成一個array. [https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/keys](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)

5. deepCopy每對key/value到新object. 使用 `Object.assign` [https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/assign](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

### 常見case - Loop Array 或 JSON/Map/Dictionary 時要小心的事情

有一個常見的use case是: 一個Array要挑出某個特定的element, 然後把它從這array裡移除掉. How?
