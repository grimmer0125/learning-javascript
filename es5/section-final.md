### JavaScript重點以及跟其他語言差異處

1. function除了直接呼叫外, 同時也可以是物件的類constructer function, `this`的觀念 (使用`new`), 及使用`bind`來改變this指向的object. 是其它語言比較沒有的.
2. 當直接呼叫function時(沒有使用`.` or `new` or `={}` or `bind/call/apply`時)，`this`是指到global物件.
3. 可使用object literal notion, `{}` 來當做基本類型`JavaScript Object`的定義. 若{}沒有包含function, 就變成一般的JSON資料了.
4. global scope對應到一個global object.
5. function內部包含其他function宣告(nested function), 其他語言可能有類似但沒有這麼直接.
6. object可runtime執行時輕易動態擴充member (ES5 way)
7. 多了 `===` 這個operator
8. 沒有`private`關鍵字
9. JavaScript沒有`C` type的pointer跟`C#/Java` 其reference的id.
