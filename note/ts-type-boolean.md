# ts-type-boolean

boolean 有兩個子型別

boolean 通常不會自己宣告，用推斷的就好

- true
- false
上面這種以特定值為型別的 type 稱作 [[type-literal]]

例如：

```ts
let a = true //boolean
const b = true //true
```

因為 b 是用 const 宣告的，值不會變，所以會用更精確的定義把 b 的 type 定義成 true
但 a 是用 let 宣告的，值可能會變，所以只是 boolean