# ts-type-enum


> Enum 慣例用大寫開頭，Key 也是大寫開頭
> 
enum 和其他單純標註性的語法不一樣
enum 除了宣告型別之外，還是一個合法的宣告語法，會在 JS 內直接建立一個 object，取值也和 object 一樣

首先先來看 enum 無 value 的 enum，



```ts
enum Language{
    English,
    Chinses,
    OK
}
```
這個東西會被 compile 成下面的 JS 


```js
var Language;
(function (Language) {
    Language[Language["English"] = 0] = "English";
    Language[Language["Chinses"] = 1] = "Chinses";
    Language[Language["OK"] = 2] = "OK";
})(Language || (Language = {}));
```
從這樣來看，我們發現


```ts

```

`Language[Language["English"] = 0] = "English";`
enum 會建立 Object 並新增屬性
1. 且 Key 為你建立的 Key，value 會是建立的 index
2. 另外建立一個 key 為 index，value 為 key 的 屬性

換句話說，Enum 會建立一個雙向的查找，對於 enum item 跟 index



如果 value 是數字

```ts

enum Num {
    one =  1,
    two = 50,
    three
}
```
```js
var Num;
(function (Num) {
    Num[Num["one"] = 1] = "one";
    Num[Num["two"] = 50] = "two";
    Num[Num["three"] = 51] = "three";
})(Num || (Num = {}));
```

會用同樣的道理，只是雙向查找的 value / key 會用 enum item 的 value 代替，值得一提的是 *推論*，數字的話會自動幫你推論為上一個 item index + 1


### 那麼 enum 到底做了那些事情？

```ts
enum Color {
    Red = '#ff0000',
    Yellow = '#FFFF00',
    Blue = '#0000FF',
    White = 255,
    Black = 0
}

Color[9] = '123123' //Index signature in type 'typeof Color' only permits reading.ts(2542)
Color[255] = 'NotWhite' //Index signature in type 'typeof Color' only permits reading.ts(2542)
Color['White'] = 0 //Cannot assign to 'White' because it is a read-only property.ts(2540)
console.log(Color[8])
console.log(Color[9]);
console.log(Color[255]);
```
從這段看起來蠻明顯，在 type 上會是這樣
簡單說，大概像這樣

```
type Color = {
    readonly Red: '123123' ,
    readonly Yellow: '#FFFF00',
    readonly Blue: '#0000FF',
    readonly [key:number]: 'Red' | 'Yellow' | 'Blue'
}

```



### 分割宣告
```ts
enum Color {
    Red = '#ff0000',
    Yellow = '#FFFF00',
    Blue = '#0000FF'
}

enum Color {
    Green = '#00FF00'
}
```

可以分開來宣告
不過被 compile 出來也是分割的就是

```js
(function (Color) {
    Color["Red"] = "#ff0000";
    Color["Yellow"] = "#FFFF00";
    Color["Blue"] = "#0000FF";
})(Color || (Color = {}));
(function (Color) {
    Color["Green"] = "#00FF00";
})(Color || (Color = {}));
```

### 推論
```ts
enum Num {
    one =  1,
    two = 2,
    three
}

console.log(Num.three);
```

```js
var Num;
(function (Num) {
    Num[Num["one"] = 1] = "one";
    Num[Num["two"] = 2] = "two";
    Num[Num["three"] = 3] = "three";
})(Num || (Num = {}));
console.log(Num.three);
```

會幫你推導值...


### 怪現象

```ts
enum Color {
    Red = '#ff0000',
    Yellow = '#FFFF00',
    Blue = '#0000FF'
}
console.log(Num['Red']) //Element implicitly has an 'any' type because index expression is not of type 'number'.ts(7015)

```

### const enum

下面這個情況 TS 不會報錯

```ts
enum Color {
    Red = '#ff0000',
    Yellow = '#FFFF00',
    Blue = '#0000FF',
    White = 255,
    Black = 0
}

console.log(Color[9]);
```

某方面說合理，因為 enum 只是建立一個雙向的 object，所以你還是可以存取沒在 enum 中宣告的屬性

可以用 `const enum`避免掉

```ts
const enum Color {
    Red = '#ff0000',
    Yellow = '#FFFF00',
    Blue = '#0000FF',
    White = 255,
    Black = 0
}

console.log(Color[9]); //A const enum member can only be accessed using a string literal.ts(2476)
```

但是 const enum 跟 enum 是很不一樣的

先看 compile 的結果

```ts
const enum Color {
    Red = '#ff0000',
    Yellow = '#FFFF00',
    Blue = '#0000FF',
    White = 255,
    Black = 0
}

console.log(Color['Red']);
```

```ts
console.log("#ff0000" /* 'Red' */);
```

不！const enum 根本沒有建立 object，只會直接置入在行內（inline），或者說 const enum 建立的 object 只存在編譯階段而已

這件事情可以用 ts的設定來處理讓他實際被建立 object [[tsconfig-setting#preserveConstEnums]]

如果是 const enum 的話

```ts
const enum Color {
    Red = '#ff0000',
    Yellow = '#FFFF00',
    Blue = '#0000FF',
    White = 255,
    Black = 0
}

console.log(Color['Red']);
console.log(Color[9]); //A const enum member can only be accessed using a string literal.ts(2476)
console.log(Color[0]); //A const enum member can only be accessed using a string literal.ts(2476)
```

真正的原因是 const enum 是單向的，不允許反向查找，只有 key value 的 mapping，而且也不允許用 string literal 來存取


### 雷點


```ts
const enum Color {
    Red ,
    Yellow ,
    Blue ,
    White ,
    Black
}


const print = (p:Color) => {
    console.log(p);
}

print(1) //????
print(Color.Red)

```
因為 [[ts-type-enum#那麼 enum 到底做了那些事情？]] 那個原因...所以會出現上面很怪的行為

總之不要用 enum...

不然你就得這樣用

```
const enum Color {
    Red = 'Red' ,
    Yellow  ='Yellow' ,
    Blue = 'Blue' ,
    White = 'White' ,
    Black = 'Black'
}
```

幹那我用個屁，總之別用 enum，不然至少千萬不要碰普通的 enum，只使用 const enum


## type Enum
Enum 本身除宣告一個值以外也宣告了一種型別，可以看（([[ts.concept.declaration]])），而這樣的型別代表著是 enum 中的一個屬性，而且這樣的屬性必定由 enum 本身的 property 來賦值

```ts
enum Num {
  one = "one",
  two = 2,
  three,
}

const one: Num = Num.one; //OK
const one: Num = 'one'; //error


```

> 注意， enum 的 type 是只他的 「property」而不是只 Enum 本身