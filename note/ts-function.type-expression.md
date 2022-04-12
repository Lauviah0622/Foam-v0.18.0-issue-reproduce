# ts-function.type-expression


直接宣告 function 這個東西的 type，在後面做使用

第一種比較簡短的形式

```ts
type Sum = (a: number, b: number) => number

const sum: Sum = function (f, j) {
  return f + j;
};
```
第二種比較長的形式


```ts
type Sum = {
    (a:number, b:number) => number
}

```

第二種比較長的形式可以使用 [[ts-function.overload | overload]]

除此之外，比較長的形式還可以新增 function parameter


```ts
type Sum = {
    (a:number, b:number) => number,
    isSummed: boolean
}

```
