# type-object

TS 的物件不辨別 object 本身的製作過程，不論是直接 object lotteral `{key: value}`），或者是使用 `new Constructor`，或者是 `() => ({})`，TS 的物件記錄表示著一個 object 的「形狀」，因為 JS 本身的慣例是 strutually typed([[structurally_and_nominally_typed]])。



### `:object` 宣告

```
const obj:object = {
    a: '123
}

obj.a //error
```

object 只表示這個東西是物件，不表示裡面有被定義 property

使用情境 => 
1. 你只是想要這個值被標示為一個物件
2. 你不會去操做這個物件的 property ex: `obj.a = 1` 

__proto__ 上面的東西是可以存取到的（畢竟這個沒有被定義 property 的物件也還是可以使用 prototype），所以

```
obj.toString()
```
這件事情是可以的

不過如果你硬要使用舊的語法： `__proto__` 這個東西會視為 type 上面沒有宣告 -- TS 不支援這件事情（或者是要看版本？）

### object literal syntax

意思是宣告 object 的形狀
```
const obj: {
    a: string,
    b: number,
    c: symbol,
    d: boolean
} = {
    a: '123',
    b: 123,
    c: Symbol('123'),
    d: true
}

/*
const obj: {
    a: string;
    b: number;
    c: symbol;
    d: boolean;
}
*/
```



```ts
const obj = {
    a: '123',
    b: 123,
    c: Symbol('123'),
    d: true,
    good(x: number): string,
    bad(x: number):string,
}

/*
const obj: {
    a: string;
    b: number;
    c: symbol;
    d: boolean;
    good: (x: number): string,
    bad: (x: number): string
}
*/
```

### property tag
```ts
type Obj = {
    a: string,
    b?:number,
    readonly c: boolean
    readonly [key:number]: boolean
}

const obj1:Obj = {
    a: '123',
    c: true,
    1: true,
}
obj1.c = false //Cannot assign to 'c' because it is a read-only property.ts(2540)
obj1[1] = false //Index signature in type 'Obj' only permits reading.ts(2542)

const obj2:Obj = {
    a: '123,',
    b: 123,
    c: true,
}

const obj3:Obj = {
    a: '123,',
    b: '123',
    c: true
}
```
分別有 
- optional：可選
- read-only property: `readonly`，表示唯讀，不能更改
- Index signature: `[keyName:T]: U` ，表示說 這個 object 接下來新增的屬性，其中 key 的 type 一定要為 T，value 一定要是 U。 keyName 可以自己取。這個東西可以跟 readonly 一起用

### `{}` 和 `Object`
這東西是個坑

下面的東西是合法的

```
let obj: {};

obj = 1 ;
obj = "string";
```

這東西代表任何非 null 或 undefianed 的值，但如果上面那行你有使用 `plugin:@typescript-eslint/recommended`，會報錯

> Don't use `{}` as a type. `{}` actually means "any non-nullish value".
> - If you want a type meaning "any object", you probably want `Record<string, unknown>` instead.
> - If you want a type meaning "any value", you probably want `unknown` instead.
> - If you want a type meaning "empty object", you probably want `Record<string, never>` instead.eslint@typescript-eslint/ban-types

就是叫你別用啦

這個東西用 `Object` 也是同理

