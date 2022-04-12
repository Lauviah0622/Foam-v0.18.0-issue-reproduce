# http.method


### 冪等性

[RFC 7231: 4.2.2 Idempotest Method](https://datatracker.ietf.org/doc/html/rfc7231#section-4.2.2)

>  A request method is considered "idempotent" if the intended effect on
   the server of multiple identical requests with that method is the
   same as the effect for a single such request.

RESTful 有一個很重要的性質稱作為冪等性，意思是如果這項操作（可以看做是如果發出多次 API）會不會造成不一樣的結果。

在所有的 Method 裡面 POST 和 PATCH 是不具冪等性的

POST 意味著新增資料，所以當然不具冪等性，這點很好理解
PATCH 則代表著局部的資料更新，不具冪等性這件事情可以說是定義上的
