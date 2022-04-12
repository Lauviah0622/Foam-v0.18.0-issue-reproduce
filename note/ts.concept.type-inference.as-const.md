# ts.concept.type-inference

這個 operator 會作兩件事情

1. 在 type inference 的時候停用 [[ts.concept.type-widening]]
2. 並且把值的型別作為 assertion [[ts.concept.assertion.md]]
3. 並且所有的值都標記上 readonly 的 modifier


```ts
let a = {x: 3} // {x: number}
let b: {x: 3} // {x: 3}
let c = {x: 3} as const // {readonly x: 3}
```

使用的意義上，這個應該是用在絕對不會被改變的值，像是常數那種的

