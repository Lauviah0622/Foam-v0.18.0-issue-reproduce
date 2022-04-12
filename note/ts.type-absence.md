# ts.type-absence

### null
就代表 null

### undefiend

就代表 undefined



在 strictNullChecks:false 的情況下 null 盒 undefined 是其他 primative type 的子型別，但如果在 打開的情況下
[[tsconfig-setting#strictNullChecks]] 的情況下，就不允許

```ts
type A = {
    name: string,
    age: number
}

const man:A = {
    name: '123',
    age: null //error
}
```

### void 
表示 function 不回傳值（沒有 return 的意思）ame:

### never



表示 function 不結束，ex: 

```ts
const a = (i):never => {
    while(true) {
        console.log(123)
    }
}

const b = () => {           //() => never
    throw Error("err");
    
}

```

另外，never 是一個代表沒有型別的型別，有點像值裡面的 undefined
可以看下面這個範例

```ts
type P = boolean | never //boolean
type O = boolean | void // boolean | void
```

只有 never 做得到這樣的事情，所以可以備用在 [[ts-type.condition-type]]

```ts
type Without<T, U> = T extends U ? never : T

type O = Without<boolean | number | string, string> 
// boolean | number

```



