# ts-type.operator.key-of

這個東西可以直接給出一個 [[ts.concept.shape-type|shape type]] 中所有 key 的交集

```ts

type ColorType = {
    red: 'ff0000',
    green: '00ff00',
    blue: '0000ff',
}


interface ColorInterface {
    red: string
    green: string
    blue: string

}

class Color {
    public red: string = '123'
    public green: string = '342'
    public blue: string = '1233'
}

type ColorKey= keyof Color;
type ColorKey2= keyof ColorType;
type ColorKey3= keyof ColorInterface;
// red | green | blue
```

搭配泛型的 [[ts.generic#呼叫榜定]] 我們限縮泛型的型別成為另一個泛型的 key


```ts
function get<
        O extends object, 
        K extends keyof O
    >(object: O, key: K) {
    return object[key]
}

```

甚至搭配 [[ts-type.operator.keying-in]] 來抓到 nesting object 的 key 
```ts
function get<
        O extends object, 
        K1 extends keyof O,
        K2 extends keyof O[K1],
    >(object: O, key1: K1, key2: K2) {
    return object[key1][key2]
}
```