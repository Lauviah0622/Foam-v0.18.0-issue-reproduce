# typescript.utility-Types.record

Record 表現了對應的關係
有兩種情境，通常都是用第二種比較多


```ts
type Weekday = string;
type Day = 'Weekday' | 'Sat' | 'Sun';

const nextDay:Record<Weekday, Day> = {
    Mon: 'Sun'
}

```

這樣的話基本上就和

```ts
type A = {
    [key: string]: Day 
}

```

差不多。

第二種才是精華



```ts
type Weekday = 'Mon' | 'Tue' | 'Wed';
type Day = 'Weekday' | 'Sat' | 'Sun';

const nextDay:Record<Weekday, Day> = {
    Mon: 'Sun',
    Tue: 'Weekday',
    Wed: 'Sat'
    // 'Mon' | 'Tue' | 'Wed' 三個都要有，不然會替出
    // Type '{ Mon: "Sun"; }' is missing the following properties from type 'Record<Weekday, Day>': Tue, Wed ts(2739)
}
```

如果第一個泛型會是 literal type 的交集，那麼 Record 裡面就必須要有所有的 literal 作為 key


其實 Record 本身就是使用 Maptype [[ts-type.operator.map-type]] 的 alias

```ts
type Record<K extends string | number | symbol, T> = { [P in K]: T; }
```