# ts-definition-assignment

TS 支援這種形式

```
let a:number

a = 10
```
即使再 `let a:number` 的時候，a 是 number，也不會報錯

但如果
```
let a:number

console.log(a)
```

這樣會報錯，因為 a 這個東西還沒被賦值，不符合 a 的 type

