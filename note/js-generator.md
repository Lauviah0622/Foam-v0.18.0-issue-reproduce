# Generator function 


```js
function* createGenerator() {
    let a = 0
    let b = 1
    while(b < 100) {
        yield a;
        [a, b] = [b, a + b]
    }
}
```

generator function 可以建立一個 generator。generator 是一個具有 iterable 性質的 iterator，這兩個專有名詞是什麼等等再解釋


```js
const fibGenerator = createfibGanerator();

console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())

/*
{ value: 0, done: false }
{ value: 1, done: false }
{ value: 1, done: false }
{ value: 2, done: false }
{ value: 3, done: false }
{ value: 5, done: false }
{ value: 8, done: false }
{ value: undefined, done: true }
*/

```

從上面這個可以看到， generator function 不會 return 值，而是return 建立一個 generator 物件，這個物件上面帶有 next 這個 method。

符合 iterator protocol 的 object 就稱作 iterator，有兩點
1. 有 next 這個 method
2. next 會 return `{value: any, done: boolean}`

所以 generator 是符合 iterator protocol 的，我們可以用 next 來取得下一個值

那 next 取得的值是什麼？在 generator 中，就是 yield 出來的值

在呼叫 next 的時候，會執行 generator function 的內容（注意！不是 generator function 本身），

而在 generator function 中我們可以看到 yield，可以想像成 return，但不同的是他不會終止 functino 的執行，只會暫停 function 的執行，並 return 值以及這個 generator 的狀態: `done` 表示這個 generator 能不能再繼續產生值（或者可以簡單看成 generator function 是不是真正執行完 --- 還有沒有 yield 可以執行）

像下面的例子

```js
function* createFibGenerator() {
    let a = 0
    let b = 1
    while(true) {
        yield a;
        [a, b] = [b, a + b]


        if (b > 20) {
            return 'done'
        }
    }
}

const fibGenerator = createFibGenerator();

console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())
console.log(fibGenerator.next())


/*
{ value: 0, done: false }
{ value: 1, done: false }
{ value: 1, done: false }
{ value: 2, done: false }
{ value: 3, done: false }
{ value: 5, done: false }
{ value: 8, done: false }
{ value: 'done', done: true }
{ value: undefined, done: true }
{ value: undefined, done: true }
{ value: undefined, done: true }
{ value: undefined, done: true }
{ value: undefined, done: true }
*/
```

因為 b > 10 就已經 return 了，所以 generator funtion 就不會再進行下去，自然 done 等於 true。



FAQ

generator function 是什麼？
簡單說，是一個可以建立 generator(iterable iterator) 的 function

可以想成

```js
function* createGenerator() {
    let a = 0
    let b = 1
    while(true) {
        [a, b] = [b, a + b]
        if (b > 20) {
            yield a;
        }
    }
}



function createGanetaror() {
    return {
        a:0,
        b: 1,
        [Symbol.iterator]() {
            return this
        },
        next() {
            const c = this.b
            this.b = this.a + this.b
            this.a = c
            // 因為 this 不能用單行賦值
            
            if (b > 20) {
                return {
                    done: true
                }
            } else {
                return {
                    value: b
                    done: true
                }
            }
        }
    }

}
```

但是用 generator 建立的 function 內部狀態是不可見的，應該比較接近下面，把變數藏在閉包裡面

```js
const iterableObject = {
    [Symbol.iterator]: function () {
        let a = 0
        return {
            next: function () {
                a++
                return {
                    value: a,
                    done: false
                }
            }
        }
    }
}
```

因為在 genetator functnio 裡面可以利用 yield 把多個 function 的執行 壓縮在一個作用域之中
因為 generator function 本身是
1. 可中斷（透過 yield 中斷），並可以再執行（透過執行 next）
2. 可多次 return （也透過 yield return 值）
3. 在同一個作用域當中


能不能有純 iterable 物件？

可以，只要單單實作 [Symbol.iterator] 就好，但 iterable object 只能透過使用 iterable protocol 的 js 語法來 iteration
```js
const iterableObject = {
        [Symbol.iterator]() {
            let a = 0,
            return {
                next: () => {
                    a++
                    return {
                        value: a,
                        done: false
                    }
                }
            }
        }
    }
```

能不能有純 iterator 物件？

當然也可以，但你就只能手動 call object 來拿到下一個狀態，不能使用 JS 中有 iterable protocol 的語法

```js
const iteratorObject = {
        a: 0,
        next: () => {
            this.a++
            return {
                value: this.a,
                done: false
            }
        }
    }
```

那自己建立 iterable iterator？
可以利用 this，讓 iterator return 自身

```js
const iterableIteratorObject = {
    [Symbol.iterator]() {
            return this
        },
    next: () => {
        this.a++
        return {
            value: this.a,
            done: false
        }
    }
}
```


可以再 object 內建 generator method，在 key 前面加上一個 `*`

```js
const obj = {
    *[Symbol.iterator]() {

    }
}
```

