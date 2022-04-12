# ts-type.assertion

主動指定說一個東西是什麼型別

```ts
function formatInput(input: string) {}

const getInput = (input: string | number): string | number => {
  return input;
};


formatInput(getInput('qwe') as string)
```

像上面 getInput 原本可能是 string 或者是 number（雖然是直接 return input，但我們這裡直接指定了 return 值的行別，算是把 return 的東西看作一個變數，並宣告了他的型別，而return 的值要符合這個行別 ），而我們直接透過 as string 指定了型別

> 要注意的一件事情是， assertion 只能指定自己的子型別或者是超型別

### assertion 語法

assertion 有兩種語法，一種是 `as` 一種是 `<>`

```ts
formatInput(getInput('qwe') as string)
formatInput(<number>getInput('qwe'))
```

### 適合使用 assertion 的時機

- 變數的操作不在同一個 scope，卻可以保證其中變數的型別（例如拿取閉包的變數）



### nonnull


在 expression 後面加上一個 `!`，可以告訴 TS 這個屬性一定存在，不會是 null | undefined
```ts
document.getElementById('test')! // 可以保證這個元素一定在

let a = null! //never，因為本身是 null，又排除掉 null，就是 never 了
```

用法：


```ts

type A1 =  {
    id?: string
}

function test (i: A1) {
    if (!i.id){
        return 
    }

    setTimeout(() => {
        const e = document.querySelector(i.id!) // 這邊用 ! nonnull 來判定說 i.id 一定存在
    }, 500);
}


type A2 = {id: string}
type A3 = {}
type A4 = A2 | A3

function test2(i: A4) {
    if (!('id' in i)) { //... 這個是 TS 的缺陷，你一定這裡一定要改用 'id' in i，因為 i.id 不一定存在會報錯
        return 
    }
    setTimeout(() => {
        const e = document.querySelector(i.id)
    }, 500);
    
}

```


#### 變數的 nonnull

```ts
function w2() {
    let b: string // 1. b 指定 string
    setB() // 2. 呼叫 setB()

    console.log(b.length) // 4. 存取 b.length，錯誤。Variable 'b' is used before being assigned
    function setB() {
        b = '123' // 3. 幫 b 賦值
    }
}
```

如果遇到上面這種情況，也就是透過同 scope 的 function 透過閉包賦值（TS 的罩門就是在閉包）。這邊 TS 不知道你在 setB 裡面對 B 做了什麼，ts 只會在同作用域裡面判別。

所以我們必須「手動」指定 b 這個變數就算沒有初始化也不會是 null | undefined

```ts
function w2() {
    let b!: string // 1. b 指定 string
    setB() // 2. 呼叫 setB()

    console.log(b.length) // 4. 存取 b.length，錯誤。Variable 'b' is used before being assigned
    function setB() {
        b = '123' // 3. 幫 b 賦值
    }
}

```