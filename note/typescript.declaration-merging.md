# typescript.declaration-merging

https://www.typescriptlang.org/docs/handbook/declaration-merging.html

```js

interface A {
    good(x: number): string
    bad(x: number):string
}

interface A {
    nice: number
    good(x: string): string
}

```

上面兩個會合併成

```ts
interface A {
    good(x: number | string): string
    bad(x: number):string
    nice:number
}
```

整體概念有點類似 interface 版的[[ts-function.overload]]

declaration merging 也可以用泛形，不過必須要完全一樣


