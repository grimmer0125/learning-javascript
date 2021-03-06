### 如何向Server要資料

方法種類:

1. XMLHttpRequest (一般browser內建)
2. 使用jQuery的`$.get()`, `$.ajax()`. (其也是封裝使用了XMLHttpRequest).
3. 使用Node.js或部份Browser內建的Fetch, e.g. [https://github.com/bitinn/node-fetch](https://github.com/bitinn/node-fetch)

如果要在全部的Browser上面使用Fetch, 可使用

1. Bower [https://github.com/github/fetch](https://github.com/github/fetch)), or
2. CDN [https://cdnjs.cloudflare.com/ajax/libs/fetch/1.0.0/fetch.min.js] (https://cdnjs.cloudflare.com/ajax/libs/fetch/1.0.0/fetch.min.js), 其介紹:[https://cdnjs.com/libraries/fetch](https://cdnjs.com/libraries/fetch) 來安裝.

以下是使用fetch的example, 取得github上任意帳號的資料，

~~~ javascript
fetch('https://api.github.com/users/任意帳號')
.then(function(res) {
  return res.json();
}).then(function(json){
  console.log(json);
});
~~~
