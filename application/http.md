### http response: Server routing & API/Restful endpoint

Server回http response時粗略來分有兩種:

1. Routing/Resource type (html, css, images), 
2. Restful/API type, e.g.`{name:"apple"}`.

**Routing:**
~~~
最簡單的web server: 
  收到 grimmer.io 這個http request, 回傳根目錄下的 /index.html 
  收到 grimmer.io/about.html, 回傳 /about.html
變化的:  
  收到 grimmer.io/about.html, 回傳 /assets/about.html (實際上的檔案位置)
~~~

Restful endpoint:
~~~ 
收到 grimmer.io/doc/doc1, 回傳doc1的內容，可以為XML, JSON等。 
通常是JSON, e.g. {author:"mike", content:"blahblah"}
~~~