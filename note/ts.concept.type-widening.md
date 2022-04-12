# ts.concept.type-wideing


首先，變數在宣告時如果不加干涉，會自動產生型別

```ts
let a = '123' // string
const a = '123' // '123'
```

雖然 value 一樣都是 `'123'`，但由於宣告方式不同。
- let 是可變的，所以 type 為 string
- const 是不可變得，所以 type 為 literal type: '123'

雖然都是賦值 '123' 但是 let 的型別卻會從 '123' => string，這樣的行為就稱作為 type widening

### enum

關於可變和不可變的型別推論不同，在 enum 還有下面的例子

```ts
enum E {
    X, Y, Z
}

let e = E.X // type E
const f = E.X // type E.X
```
let e => type E 代表著會是 enum E 的其中一個屬性
const f => type E.X 代表著只會是 enum E 中的 X 這個屬性

### 防止 type widening 
直接指定 literal type

```ts
let num:123 = 123 //type = 123

```

### 變數賦值的擴展

```ts
const a = 'x'       // type: 'x'
let b = a           // type string
const c = a         // type 'x'

const d:'x' = 'x'   // type 'x'
let e = d           // type 'x'
```

a 的行別雖然是 'x'，但是在賦值給 b 的時候會被拓展成 string。

不過 d 的行別也是 'x'，但是因為有指定型別，所以在賦值給 e 的即使是 let，一樣會變成 'x'

可以這樣思考，但不確定底層邏輯是不是對的

第一個情境

```ts
const a = 'x'
/*
1. 用 const 宣告了 a，a 沒有被宣告行別
2. a 被賦值了 'x'， 'x' 的型別是 'x'
3. a 沒有被宣告型別，為了產生型別而型別推論： a 本身為 const + 值為 'x' => a 不會再被賦值，推論出 a 的型別為 'x'

==> a 的型別為「推論出來的 'x'」 
 */ 

let b = a 
/*
1. 用 let 宣告了 b，b 沒有被宣告行別
2. 在「賦予值」上面：b 被賦值了 a， a 的值為 'x' 。在「賦予型別」上面：a 變數本身並沒有型別，只有被推論出來的型別，因此不執行「賦予型別」。
3. b 沒有型別，為了產生型別而型別推論： b 本身為 let + 值為 'x' => b 可能會再被賦值，推論出 b 的型別為 string

==> a 的型別為「推論出來的 string」 
 */ 

const c = a
/*
1. 用 const 宣告了 c，c 沒有被宣告行別
2. 在「賦予值」上面：c 被賦值了 a， a 的值為 'x' 。在「賦予型別」上面：a 變數本身並沒有型別，只有被推論出來的型別，因此不執行「賦予型別」。
3. c 沒有型別，為了產生型別而型別推論： c 本身為 const + 值為 'x' => c 不會再被賦值，推論出 c 的型別為 'x'

==> c 的型別為「推論出來的 'x'」 
 */ 

```

第二個情境

```ts
const d:'x' = 'x'
/*
1. 用 const 宣告了 d，另外 d 被宣告了型別 'x'
2. d 被賦值了 'x'， 'x' 的型別是 'x' => 正確，通過
3. d 已經被宣告型別，不推論

==> d 的型別為「宣告出來的 'x'」 

*/ 

let e = d 
/*
1. 用 let 宣告了 e，e 沒有被宣告型別
2.進行賦予
    a. 在「賦予值」上面：e 被賦值了 d， a 的值為 'x' 
    b. 在「賦予型別」上面：d 變數本身的型別是 'x'，因此執行「賦予型別」，e 的型別是 'x'
3. e 已經被賦予型別，不推論

==> d 的型別為「賦予出來的 'x'」 
*/ 

```

第三個情境

```ts
let f:'x' = 'x'
/*
1. 用 let 宣告了 d，另外 d 被宣告了型別 'x'
2. d 被賦值了 'x'， 'x' 的型別是 'x' => 正確，通過
3. d 已經被宣告型別，不推論

==> f 的型別為「宣告出來的 'x'」 

*/ 

let g = f
/*
1. 用 let 宣告了 g，g 沒有被宣告型別
2.進行賦予
    a. 在「賦予值」上面：g 被賦值了 f， f 的值為 'x' 
    b. 在「賦予型別」上面：f 變數本身的型別是 'x'，因此執行「賦予型別」，g 的型別是 'x'
3. g 已經被賦予型別，不推論

==> g 的型別為「賦予出來的 'x'」 
*/ 

```

### 賦值 nulL | undefined

會被拓展成 any


在書上有提到一個例子：
```ts
function x() {
    let a
    a = 1
    a = '1'
    return a
}

let a = x() // string
```


這個東西在 [[ts.concept.type-inference.return-reinference]]


### freshness 

[[ts.concept.type-widening.freshness.md]]

