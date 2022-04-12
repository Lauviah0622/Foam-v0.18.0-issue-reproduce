# ts-function


## 不同 function 以及參數的的表示方法

基本
```ts

function add(a: number, b:number) {
    return a + b
}


```

 return 值註釋

 ```ts

function add(a: number, b:number):number {
    return a + b
}

```

arrow function

```ts
const add = (a: number, b:number) => {
    return a + b
}
```

### optional parameter


```ts
const add = (a: number, b?:number) => {
    return a + b
}
```

### default parameter
```ts
const add = (a: number, b:number = 123) => { //Type number trivially inferred from a number literal, remove type annotation.eslint@typescript-eslint/no-inferrable-types
    return a + b
}
```

會自己幫你推斷，不用加
```ts
const add = (a: number, b = 123) => {
    return a + b
}
```

不過有其他性可能還是可以加
```ts
const add = (a: number, b:number | string = 123) => {
    return a + +b
}
```

### rest parameter

```ts
const sum = (...params: number[]) => {
    return params.reduce((prev, num) => prev + num)
}
```


optinal 跟 default 不能一起用，畢竟你給 default 就代表那個參數 optional 了


### this parameter
```ts
function addThisNumberTen(this:number) {
    return this.number + 10
}
```
this 放在第一個有特別的意思，可以指定 this 的型別。

不過這個東西在 arrow function 不管用，因為 arrow function 沒有 this

正常的模式裡面如果上面並不會報錯，可以開啟 [[tsconfig-setting#noImplicityThis]]
 

### generator

generator function 的 type 是 `Generator` 
產生出來的 object 的 type 會是 IterableIterator<>

## function type syntax

`Function`

泛指所有的 function，不要用這個

### Function Type Expressions
[[ts-function.type-expression.md]]


### contextual typing
```
function times(f: (i: number) => void, n: number) {
  for (let i = 0; i < n; i++) {
    f(i);
  }
}

times((i) => {console.log(i)}, 10)
```

下面在 tiems() 使用 arrow function 不用再次宣告型別，因為在 function times 裡面已經宣告過了

或者換一個方法來看，在 times() 那裡使用 arrow function 本身並沒有建立一個 function，只是域 arrow funcion syntax 「產生」 一個 funtion 而已。型別宣告只需要在變數 "宣告"的部分才宣告


### overload 

[[ts-function.overload.md]]


### generic 
泛型

[[ts.generic.md#function 的 generic]]








