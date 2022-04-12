# ts-type-nubmer

基本上就是所有數字的集合，包含
- `Infinity`
- `-Infinity`
- `0`
- `-0`
- `NaN`
- 整數
- float number

通常也不太會自己宣告，都是給 TS 推斷

[[js_number_]]
有個特別的地方
`Infinity`, `-Infinity`, `NaN` 不能作為 type literal
語法層面上不支援

原因看起來在這邊 [https://github.com/microsoft/TypeScript/issues/15135](https://github.com/microsoft/TypeScript/issues/15135)

似乎是在判斷邏輯上會變很麻煩，但[這篇 issue](https://github.com/microsoft/TypeScript/issues/32277) 裡面又 Infinity 這件事情沒有像 NaN 這個東西那麼複雜

不過也有很 tricky 的方式可以實現：[https://github.com/microsoft/TypeScript/issues/31752](https://github.com/microsoft/TypeScript/issues/31752)

### numeric seperator


JS 裡面可以用 [[js-numeric-separator]]，TS 也可以

```ts
const num:100_00000_00 = 1000000000
```