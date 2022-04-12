# ts.concept.narrow.truthiness

在 JS 裡面，只要會判斷出 true/false 的地方都可以帶入任何值，JS 會隱式轉換（自動轉換）成 boolean 的結果，像是

- if (), else if ()
- ..? ..: ..
- &&, ||
- !

所以任何值轉化成 boolean 的結果在 JS 裡面雖然沒有一個專有名詞，但我們可以稱之為 truthiness

-   `0`
-   `NaN`
-   `""` (the empty string)
-   `0n` (the `bigint` version of zero)
-   `null`
-   `undefined`

除了這些以外全部都是 true

## 顯式轉換手動

除了上面的隱式轉換以外，我們也會利用一些方法來手動把值轉換成 boolean

- `Boolean()`
- `!!`

這兩個東西在 TS 裡面會有不同的行為

```ts
// both of these result in 'true'
Boolean("hello"); // type: boolean, value: true
!!"world"; // type: true,    value: true
```

雖然兩個都會在 jS 中被轉化成 true，但是在 TS 的 narrow 過程會是不同的東西，Boolean 會給一個 boolean type，但 !! 則會給一個精確的 true
換句話說應該要多用 !! 囉