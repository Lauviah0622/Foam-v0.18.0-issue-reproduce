# ts-execute-step

[[lang-execute-step]]

跟上面的不一樣， TS 是

1. 寫 TS 檔案（text code）
2. 產生 TS AST，在這一步會執行 型別檢查
3. compile 成 JS code，而不是 bytecode

然後就和正常的 js 一樣

4. JS 會 compile 成 JS AST
5. AST => bytecode
6. bytecode 被 runtime 執行


[[ts-compiler-idea]]