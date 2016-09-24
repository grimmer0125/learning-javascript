## strict mode

[https://msdn.microsoft.com/zh-tw/library/br230269(v=vs.85).aspx](https://msdn.microsoft.com/zh-tw/library/br230269(v=vs.85).aspx)

*檢查程式碼錯誤時，使用 strict 模式可獲得較佳的效果。例如，當您使用 strict 模式時，就不能使用隱含宣告的變數或將值指派給唯讀屬性，也不能為無法擴充的物件添加屬性。本主題稍後的程式碼在 strict 模式下的限制一節中會列出這些限制。如需 strict 模式的詳細資訊，請參閱 ECMAScript 語言規格，第 5 版。*

### web worker:

[https://developer.mozilla.org/zh-TW/docs/Web/API/Web_Workers_API/Using_web_workers](https://developer.mozilla.org/zh-TW/docs/Web/API/Web_Workers_API/Using_web_workers)

### 匿名函數的變數提升 (var hoisting)

~~~ javascript

(function(){

 console.log(a); // ouput -> undefined

 var a = 100;
 console.log(a); // 100

})();

~~~

[http://kuro.tw/posts/2015/07/08/note-javascript-variables-declared-with-the-scope-scope/](http://kuro.tw/posts/2015/07/08/note-javascript-variables-declared-with-the-scope-scope/)

因為在匿名函數獨立的 scope 內，不管 var 是放在最前面，或是最後一行，他的變數實體在該 code block 一開始就是新的了，也就是說，剛剛的 code 其實等同下面這段

~~~ javascript

(function(){

 var a;
 console.log(a); // undefined
 a = 100;
 console.log(a); // 100

})();

~~~
