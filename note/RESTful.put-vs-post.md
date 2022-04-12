# RESTful: put-vs-post

主要是 put 有冪等性
送一百次請求的結果是一樣的
而且 Put 有完全更新的意思

但是 Patch 沒有
所以 Patch 語意上可以做到下面的 api，依照 payload 新增特定數量

```
PATCH /add
{
    quantity: 12
}
```
但不適合使用 patch 來做，或者會變成完全另一個意思


除此之外，put 意味著「完全更新」資料
但 Patch 有只更新部分內容的意思

所以下面兩隻的 API 會有完全不同的結果，即使是同一支 API



```
source data 
{
    name: 'pete',
    age: 12,
    job: 'worker'
}
```

```
PUT /data
{ name: 'Jacob' }

=> {
    name: 'Jacob'
}
```

```
PATCH /data
{ name: 'Jacob'}

=> {
    name: 'Jacob',
    age: 12,
    job: 'worker'
}
```

要注意一點，冪等性這件事情是嚴格寫在 [RFC](https://datatracker.ietf.org/doc/html/rfc7231#section-4.2.2) 上面的，也就是這是 [[http.method.md|HTTP Method]]  的定義內容 ，但是在意義上並不是，這是屬於 [[RESTful]] 的內容


reference:
- [“一把梭：REST API 全用 POST”](https://coolshell.cn/articles/22173.html)