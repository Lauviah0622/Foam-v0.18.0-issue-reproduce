# type_system 

型別系統有兩種
- 顯式宣告
- 程式字型推斷

宣告和推斷這兩件事情又會分別能夠再不同的地方被處理，分別是 compile（編譯） 階段以及 runtime（執行）階段

有以下幾種處理型別的方式

1. 在 "runtime" 時期來"推斷"型別：JS, Rudy, Python
2. 在 "編譯" 時期來"推斷"型別： Haskell, Ocaml
3. 需要顯示＂宣告＂型別，但是會在"compile" 時期來＂推斷＂沒有被宣告的型別：Scala, TS
4. 需要顯式宣告所有型別，並且會在 compile 時檢查：Java, C

換句話說
1. 完全不用自行宣告型別，全部由程式自行判斷（在 runtime），這應該就是所為的弱型別？
4. 全部都要自行宣告：這就是強型別？

2.還有 3. 的 分別我就沒有很清楚，聽起來 2. 是在很不明顯的時候才要加，但是加上型別會影響程式的執行方式？

但是 3. 就不會，型別只是在 compile 做檢查而已？我不太確定



---

P. 7
