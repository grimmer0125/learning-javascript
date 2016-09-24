## 基本的 Control Statements

**以下的講解大部份的程式語言也適用**

### 關於 &&

所以下面的例子來講

1. **如果左邊的expression1回傳false, 則右邊的expression2不會被執行到, 提早判斷為false**
2. **如果左邊的expression1回傳true,  則右邊的expression2會被執行到, 也是true的話整體才算是true, 不然為否**

~~~ javascript
var expression1 = function(){
  return true;
}
var expression2 = function(){
  return true;
}
// 亦可先把結果assign到一個變數
// var combine =  expression1() && expression2();
if(expression1() && expression2()) {

}
~~~

### 關於 ||

所以下面的例子來講

1. **如果左邊的expression1回傳false, 則右邊的expression2會被執行到, 只要任一個為true,整體就算是true**
2. **如果左邊的expression1回傳true,  則右邊的expression2不會被執行到,提早判斷為整體為true**

~~~ javascript
var expression1 = function(){
  return true;
}
var expression2 = function(){
  return true;
}
// 亦可先把結果assign到一個變數
// var combine =  expression1() || expression2();
if(expression1() || expression2()) {

}
