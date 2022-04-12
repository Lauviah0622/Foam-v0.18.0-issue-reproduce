# type-literal


中文翻譯：型別字面值


定義

只代表單一個值得型別，例如

```ts
let boo:true = true; //true
let num:123 = 123; //123
let str:"nope" = "nope" //"nope"
```

除了直接定義，在 TS 裡面也可以藉由 const 來推斷出 type literal，因為 const 本身不會變，如果 const 後面接上 primitive type 的值，就會推斷出 type literal

```ts
const boo = true; //true
const num = 123; //123
const str = "nope"; //nope
```

這功能 Java 沒有ㄎㄎ，蠻多語言沒有的



