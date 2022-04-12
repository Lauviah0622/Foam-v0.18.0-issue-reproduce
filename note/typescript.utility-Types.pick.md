# typescript.utility-Types.pick

```ts
type RGB = {
    red: string
    blue: number
    number: string
}

type OnlyBlueRed = Pick<RGB, 'red' | 'blue'>
/*
type OnlyBlueRed = {
    red: string;
    blue: number;
}
*/
```


會 iterate 裡面的屬性，挑出來


```ts
type MyPick<T, K extends keyof T> = { [P in K]: T[P]; }
```

