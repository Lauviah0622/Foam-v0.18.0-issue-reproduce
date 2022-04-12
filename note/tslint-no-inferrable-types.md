# tslint-no-inferrable-types

有個有趣的錯誤：

```ts
let num:number = 10
```

這個東西會觸發 [no-inferrable-types](https://typescript-eslint.io/rules/no-inferrable-types/)

簡單說就是你太廢話了，不需要自己再宣告一次

這個東西有兩個設定


```
interface Options {
  ignoreParameters?: boolean;
  ignoreProperties?: boolean;
}
```

### ignoreParameters

會忽略掉 function 參數的情形，例如

```
function foo(a: number = 5, b: boolean = true) {
  // ...
}
```

因為已經給 default，所以宣告型別是廢話。應該也只有至個情形吧



### ignoreProperties
自己去看吧

