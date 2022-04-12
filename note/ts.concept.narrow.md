# ts.concept.narrow


[narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

narrow 這件事情是一個寬鬆的型別會因為操作被現縮成更嚴謹的型別

### if 
利用 if 來縮小 type 可能的範圍：
可能的幾種方式
- [[ts.concept.narrow.truthiness.md | truthiness]]:if 內部產生的 booLean 值來判斷
- equalty
- in

### assignment

賦值也會改變行別


```ts
let x = Math.random() < 0.5 ? 10 : "hello world!";
// x: string | number
   
x = 1;
// x: number
 
console.log(x);
           
x = "goodbye!";
// x: string
 
console.log(x);

x = false; // Type 'boolean' is not assignable to type 'string | number'.
           
```
這裡有個觀念。一個直「可以被賦予」的行別是在宣告的時候被指定的，所以上面的 X 的行別會是 `string | number`，所以這個變數可以被 assign 為 number 或者是 string。

這個觀念類似於 [[ts.concept.type-widening#變數賦值的擴展]] ，變數值的賦予以及型別的賦予是分開的

但即使他被賦予為 number，本身的 type 也變成了 number，但這個「可以被賦予的行別」一樣是不變的，所以一樣可以被賦予為 string


### union type 內部的 narrow

[[ts.concept.narrow.union-type.md]]

### predicate 斷言

[[ts.concept.narrow.predicate.md]]


### type-predicate

[[ts.concept.narrow.type-predicate.md]]


