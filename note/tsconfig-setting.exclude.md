# tsconfig-setting



exclude 表示忽略 incldue 中解析的的檔案

不過這是表示自動的解析。

> Important: exclude only changes which files are included as a result of the include setting. A file specified by exclude can still become part of your codebase due to an import statement in your code, a types inclusion, a /// `<reference` directive, or being specified in the files list.

相上面說的，如果用一些方式手動的引入還是會被解析