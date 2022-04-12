# tsconfig-setting


```json
{
    "compilerOptions": {
        "lib": ["ES2015"],
        "module": "commonjs",
        "outDir": "dist",
        "sourceMap": true,
        "strict": true,
        "target": "ES2015"
    },
    "include": [
        "src"
    ]
}
```

### compilerOptnions

compiler 的設定

### lib 

環境有哪些 API。

包含可能有 node, DOM, 不同的 ES 標準，甚至不同的 lib？

### module
JS 的 import module 形式

### outDir
output 資料夾

### include
要 compile 的資料夾

### strict
嚴格模式，應該是所有的 code 都要有合理的型別，目前難理解

### noImplicitAny
如果推斷出來有 any 的 type，就會進行報錯
在 strict 模式自帶這個選項

### target 

輸出的 JS 版本


### strictNullChecks
default: 在 strict 打開的情況下 true，其他為 false

在 false 的情況下，undefined 還有 null 會是 primary type 的子型別，true 的話就不行

![picture 1](https://i.imgur.com/AinsVED.png)  

### strictPropertyInitialization



### preserveConstEnums



```ts
const enum Color {
    Red ,
    Yellow ,
    Blue ,
    White ,
    Black
}

console.log(Color['Red']);
```


true：實際 compile 初 const enum
```js
var Color;
(function (Color) {
    Color[Color["Red"] = 0] = "Red";
    Color[Color["Yellow"] = 1] = "Yellow";
    Color[Color["Blue"] = 2] = "Blue";
    Color[Color["White"] = 3] = "White";
    Color[Color["Black"] = 4] = "Black";
})(Color || (Color = {}));
console.log(0 /* 'Red' */);
```

false：直接 inline
```
console.log(0 /* 'Red' */);
```

### strictBindCallApply

strict mode 預設開啟

打開之後才會幫你做 bind call apply 的檢查

```ts
// With strictBindCallApply on
function fn(x: string) {
  return parseInt(x);
}
 
const n1 = fn.call(undefined, "10");
 
const n2 = fn.call(undefined, false);
Argument of type 'boolean' is not assignable to parameter of type 'string'.
```

Otherwise, these functions accept any arguments and will return any:
```ts
// With strictBindCallApply off
function fn(x: string) {
  return parseInt(x);
}
 
// Note: No error; return type is 'any'
const n = fn.call(undefined, false);
```

### noImplicityThis



strictmode : default true

不開啟好像不會 check this 的值，下面這個 case 不會有錯誤


```ts
  function addThisNumber() {
      console.log(this.number);
    return this.number + 10;
  },

const r = obj.addThisNumber.call({ number: "123" });
console.log(r);

```

開啟後有用到 this 的地方會強制使用 [[ts-function#this parameter | this parameter]]


### noImplicitReturns

會執行 [[ts.concept.totality | totality]] 的檢查