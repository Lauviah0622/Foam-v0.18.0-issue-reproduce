# ts.concept.variance

variance 指的是變異性。白話來說，就是兩個 type 之前的寬鬆或者嚴謹的比較程度　

舉個例子：
```ts
type A = string

type B = string | number

type C = string | number | null
```

A, B, C 三個 type 之間有寬鬆程度的比較。A 只能是 string，相對於 B 可以是 string 或者是 number，A 會比較嚴謹。而同樣的道理 B 又比 C 還要嚴謹。我們可以排出一個嚴謹（寬鬆）程度的順序為

A <: B <: C (A 最嚴謹，B 次之，C最寬鬆)

而在型別系統中，
有些地方我們可以帶入比定義的型別更加嚴謹的型別進去，這樣的地方我們稱之為有「協變性」 covariance
那如果我們可以帶入更加「寬鬆」的型別進去，這樣的地方我們稱之為有「抗變性」 contravariance


子行別：超型別的概念




[[ts.concept.variance.function.md]]