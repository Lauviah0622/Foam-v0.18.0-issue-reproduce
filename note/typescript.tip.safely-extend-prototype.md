# typescript.tip.safely-extend-prototype


1. 利用 [[typescript.declaration-merging]] 來擴充行別
2. 執行擴充的內容，這裡用 [[ts.type-tuple#自動建立 tuple 型別推斷|tuple]] 執行產生更清楚的型別


```ts
function  tuple<T extends unknown[]>(...args: T) {
    return args
}

interface Array<T> { // 1. 擴充內建的型別
    zip<U>(list: U[]):[T, U][]
}

Array.prototype.zip = function<T, U>(this: T[], l: U[]): [T, U][] {
    return this.map((v, i) => tuple(v, l[i])) // 用 tuple 來建立更精準的描述
}

```
這個情況是建立在 這個 js file 完全不是 module 模式才可以使用。如果是 module 模式，必須要用 global namespace 才可以宣告全局型別

```ts
import //...

declare global { // 裡面都是全局型別
    interface Array<T> {
        zip<U>(list: U[]):[T, U][]
    }
}

export //...

```



## 注意事項


不過要注意的一點是型別本身是直接宣告在 global 的，即使沒有 import 我們一樣可以用 .zip 這個 type

所以我們可以把 .zip 這個檔案加進去 [[note/tsconfig-setting.exclude]]
