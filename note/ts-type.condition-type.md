# ts-type.condition-type


## condition type

```ts
type IsStringOrNumber<T> = T extends string ? string : number;

type A = IsStringOrNumber<'123'>
type B = IsStringOrNumber<123>
```

簡單說 condition type 會回傳給你 condition 其中之一的 type

## 分配率

如果 condition type 給的 generic 是一個 union type 呢？

```ts
type IsStringGetNumberButBoolean<T> = T extends string ? number : boolean;

type D = IsStringGetNumberButBoolean<'123'>
type Q = IsStringGetNumberButBoolean<123>

type H = IsStringGetNumberButBoolean<'123' | 123>
```

結果會是這樣

```ts
type H = IsStringGetNumberButBoolean<'123'> | IsStringGetNumberButBoolean<123>
```

這個就是 condition type 的分配率


## use case

[[ts-type.condition-type.usecase.md]]

## infer

[[ts-type.condition-type.infer.md]]