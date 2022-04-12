# ts.type-tuple



```ts
const tuple:[string, number, boolean] = ['123', 23, true]
```

基本觀念：固定各個位置是甚麼的 array

跟 object 一樣，也可以用 [[ts-type-object#property tag| 的 optional]]

```
type optionalTuple = [string, number, boolean?]

const tuple1:optionalTuple = ['123', 23, false]
const tuple2:optionalTuple = ['123', 23]
```

也可以用 readonly，不過用法不太一樣


```ts
type readonlyTuple = Readonly<[string, number, boolean?]>
type readonlyTuple2 = readonly [string, number, boolean?]
type readonlyTuple3 = ReadonlyArray<string>

const tuple3:readonlyTuple = ['235', 123];
tuple3.push(123) //err

const tuple4: readonlyTuple = ['123', 123];
tuple4[1] = 123 //err
```

### 自動建立 tuple 型別推斷

如果你建立一個 JS 意義上面的 tuple，他會幫你依照 array 的邏輯下去推斷

```ts
let a = [1, true]  // (number | string) []


```

但其實很多時候我們希望的型別會幫我們推斷成下面這樣，是各個位置會是什麼行別
```ts
let a = [1, true]  // 希望是 [number, boolean]
```

你沒辦法利用 [[ts.concept.assertion.md]] 來做到這點，因為會變成

```ts
let a = [1, true] as const // [1, true]
```

這時候可用一個小撇步

```ts

function  tuple<T extends unknown[]>(...args: T) {
    return args
}

let c = tuple('123', true, 123)
```

#toBeClarify 為什麼會這樣！！

