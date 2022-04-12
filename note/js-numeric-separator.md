# js-numeric-separator



可以用`_`來分隔數字，會比一堆沒分隔的 0  還要清楚

```
const number = 1000_000_000
```
話說 seperator 不一定要間距相同，例如
```js

const num = 1000_00_000_0000
```
不只有十進制可以這樣表示，其他也可以

```js
// separators in decimal numbers
1_000_000_000_000
1_050.95

// separators in binary numbers
0b1010_0001_1000_0101

// separators in octal numbers
0o2_2_5_6

// separators in hex numbers
0xA0_B0_C0

// separators in BigInts
1_000_000_000_000_000_000_000n
```

感覺比較像數字中間的 `_` 符號會被忽略的感覺

是可以的

[mdn | numeric seperator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#numeric_separators)


TS 也能做標記 [[ts-type-nubmer]]