# ts.type-array

```ts
const arr = ['str'] // 直接被推斷成 string[]
arr.push(123) //error
const arr2 = [1] //number[]
const arr3 = ['str', 1] //(string|number)[]


const arr4:(booelan | number)[]
```

大概是這樣，或者是可以用

```ts
const arr4:Array<boolan | number>
```

不過 array 有一些很特別的行為（可能也不是只有他有）

一個未指定指定 type 的 array 在被填充的時候會被慢慢 擴展 type，而 tpye 在離開自己的作用與的時候會被固定，就不能再被進行擴展

```ts

const creator = () => {
    const str = []
    str.push(1)
    str.push('123')
    str.push(true)
    return str
}


const f = creator() //(string | number | boolean)[]
f.push({}) //error

```

