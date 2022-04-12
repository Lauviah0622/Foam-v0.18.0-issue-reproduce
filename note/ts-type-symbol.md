# type-symbol

Symbol 在 JS 表示一個比對起來永遠 !== 的值

在 TS 裡面如果賦值 symbol 給 let (var)的話，type 會是 Symbol

```ts
let sym = Symbol('1'); //typeof a
```
這裡 typeof symbol 的意思是，sym 這個變數只能給她 symbol，所以可以接受的操作是

```ts
let sym = Symbol('1'); //typeof symbol
sym = Symbol('2') 
sym = Symbol('1')
```

### unique symbol

但是如果是賦值給 const，情形會不一樣

```ts
const sym = Symbol('1'); //typeof sym
```

因為 const 本身不能再被賦值，所以 sym 這個變數的 type 會直接是 typeof sym，也就是這個值只能是 sym 這個變數自己被賦值的值

這種情形叫做 unique symbol

「變數」本身的值絕對不會改變（因為是 const），而且這個值永遠不會跟其他的 unique symbol 一樣
把 symbol 本身的唯一性轉嫁到變數上面，讓變數產生了唯一性：
可以和其他沒有唯一性的東西相等（這個東西第一次理解不太直覺）

ex 
```ts
const a:unique symbol  = Symbol('1') //type a

const b = a; //這裡會是 type symbol，而不是 type a 
```

> #toBeClarify
> 為什麼上面那個不是 type a？只是 type symbol
>
> 因為上面的行為是的 b 的型別是 any（沒有被設定），然後被被賦值為 a。
> 這件事情是給 b Symbol('1') 這個值，而不是 a 這個變數，所以才會是 symbol

```ts
const a:unique symbol  = Symbol('1')

const b:typeof a = a; //typeof a 
```
這樣就會是 typeof a


不過如果是下面這樣
ex 
```ts
const a:unique symbol  = Symbol('1') //type a

const b:unique symbol = a; //Type 'typeof a' is not assignable to type 'typeof b'
```
就會報錯，目前的理解是 b 的 type 要是 b，所以只能給她 b 不能給他 a

unique symbol 這件事情理解成讓變數本身成為一種型別的感覺，但值必須要是 symbol（這樣才能符合 JS 比較的唯一性）

[[ts-idea-split-variable-value]]