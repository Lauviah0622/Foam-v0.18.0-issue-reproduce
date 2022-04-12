# ts-type.operator.map-type

https://www.typescriptlang.org/docs/handbook/2/mapped-types.html

map type 本身會 iterate 所有 union literal type 作為 key，然後要求一定要使用在 shape of type 裡面

```ts
type Weekday = 'Mon' | 'Tue' | 'Wed';
type Day = 'Weekday' | 'Sat' | 'Sun';

type DateTime = {
    [K in Weekday]: Day
}
```

K 會去 iterate 所有 Weekday 的可能性，然後把他定義進 DateTime 裡面，所以就會變成

```ts
type DateTime = {
    Mon: Day,
    Tue: Day,
    Wed: Day,
}
```

有一點需要注意， Map type 本身就屬於 [[ts-type-object]] 的 index signatures。所以只能存在一個，後面也不能再用 index signatures

## Modifier

map-type 最大的價值是可以從原本的 shape type 加以修改。所以很常搭配 [[ts-type.operator.key-of]] 來使用，例如

```ts

type RGB = {
    red: string
    blue: number
    number: string
}

type NumberRGB = {
    [key in keyof RGB]: RGB[key]
}

type OptionalRGB = {
    [key in keyof RGB]?: RGB[key]
}

type ReadonlyRGB = {
    readonly [key in keyof RGB]: RGB[key]
}

type NotReadonlyRGB = {
    -readonly [key in keyof ReadonlyRGB]: RGB[key]
}

type NotOptionalRGB = {
    [key in keyof OptionalRGB]-?: RGB[key]
}

```

我們可以用幫 property 新增 modifier（直接加或者是很多於的補一個 + 在前面），或者是用 `-` 來除去 modifier
