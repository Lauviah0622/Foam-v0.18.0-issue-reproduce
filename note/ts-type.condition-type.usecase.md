# ts-type.condition-type.usecase

透過 condition-type 的特性可以作很多非常酷的東西


## Without
```ts
type Without<T, U> = T extends U ? never : T

type O = Without<boolean | number | string, string>
// boolean | number
```

## Include 

```ts
type IsInclude<T, U> = T extends U ? T : never

type P = IsInclude<boolean | number, number> // number
type J = IsInclude<boolean | number, string> //never
```