# ts-idea-split-variable-value

從 [[type-symbol#unique symbol]] 這個地方來看，TS 的型別推斷以及賦值兩件事是要分開看得，而且是賦值優先再來判斷型別

可以說是這樣
1. 創建變數
2. 有形別 => 給予變數型別
3. 沒型別 => 保留 any
5. 依照 = （賦值運算子）右側的 operand 給予型別

#toBeClarify
注意注意注意，TS 從來沒有真的賦值下去過，因為 TS 本身就是不執行r

