## Callback function

**下一個章節有一些進階的callback的例子**

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

callback有分需要用到this, 以及沒有需要用到this的case.即上述兩例, 後面的sections會詳細講解this.
