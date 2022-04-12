# ts-type-unknown


unknown 在限制上和 any 一樣，是所有的 type 的聯集
但是在意義上不同，代表type 是「未知」，可能會在之後被進行運算或者再定義（refine）
也因為這樣，unknown 支持的操作只有 `||`, `&&`, `===` 等等比較的操作

相較之下 [[ts-type-any|any]] 的意義就不一樣，代表著可以是任意型別




```ts
let a: unknown = 30
let b = a === 123
let c = a + 10 //3.

if (typeof a === 'number') {
    let d = a + 10
}
```

TS 本身不會有自行型別推斷成 unknown 的情況。
除了很奇怪的 function，例如
```ts
const a: unknown = 30

let r = ((v) => v)(a)
```

其實應該也沒有任何運算可以產生 unknown type，執行 function 基本上都會有確定的結果

上面的 3. 會出問題，就像上面講的
> unknown 支持的操作只有 `||`, `&&`, `===` 等等比較的操作
所以不支持 `+` 這個 operator 的操作