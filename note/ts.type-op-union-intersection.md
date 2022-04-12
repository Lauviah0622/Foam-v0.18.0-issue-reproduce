# ts.type-op-union-intersection

我一開始以為是這樣

```ts
type Dog = {
    name: string,
    age: number
}

type Cat = {
    name: string,
    purrs: string

}

//一定要兩邊都有
const animal: Dog | Cat = { 
    name: 'pete',
    purrs: 'meow',
    age: 12
}
```

但不是，上面那個應該是 Intersection 聯集

```ts
//一定要兩邊都有
const animal: Dog & Cat = {
    name: 'pete',
    purrs: 'meow',
    age: 12
}
```

如果是 Union 聯集的話，下面三個都符合狀況

```ts
// 屬於 Cat
const animal1: Dog | Cat = {
    name: 'pete',
    age: 12
}


// 屬於 Dog
const animal2: Dog | Cat = {
    name: 'pete',
    purrs: 'meow',
}

// Both
const animal3: Dog | Cat = {
    
}
```

順帶一提 union 很常跟 array 一起用

```ts
type Arr = (string|number)[]
```


#toBeClarify
如果我要確定的
type A or type B，而不是是 type A | B 的話，我應該要怎麼寫

```ts

```