# ts-type-any

any 的型別是所有型別的聯集
意義上則是可以是任意型別，這點和 [[ts-type-unknown|unlnown]] 不一樣


一個變數被宣告時如果沒有賦值，也沒有被宣告型別，那他的 type 會是 any

```ts
let a // any

```