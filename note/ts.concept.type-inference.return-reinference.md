# ts.concept.type-inference.return-reinference

我不知道這個東西的確切名稱叫做什麼，先稱呼他為 return narrowing

兩個例子

```ts
function i() {
    let a
    a = '1' // any
    return a // string
}

let p = i()
```

在 i 的例子，在使用 return operator 的時候，我們就可以看到 a type 已經是 string 了。
一個值在用 let 宣告但沒有賦值的時候會是 any
但是這樣的情形在 return 時會被再次推論，所以依照 let + 值為 '1' 而推論出 a 的型別為 string


```ts
function x() {
    let a
    return a // type = undefined
}

let u = x()
```

