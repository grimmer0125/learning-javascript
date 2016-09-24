## 工具準備

### Debugger工具

* 印log: 
    1. console.log("error:", json); 
    2. console.log("msg:"+"string"); 
    3. console.log("err:%s", message), 
    4. console.error(on chrome/node.js).
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
