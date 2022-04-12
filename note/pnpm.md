# pnpm 


### global-package
新增 global package

```
pnpm add react react-dom -w
```

`-W`，`--ignore-workspace-root-check` 的意思是 [ignore-workspace-root-check](https://pnpm.io/cli/add#--ignore-workspace-root-check--w) ，會忽略 mono repo 中的不同 workspace 檢查。


不過這個 `-W` 不確定是不是所有的指令都可以用


### package.json 設定

記得要在 import 跟 exprot 的 package.json 都加上 type module


### pnpm dlx

在 npm 裡面，可以直接透過 npx 來從 registry 抓東西，然後直接執行。像是捰們平常常用的。

```
npx create-react-app my-app
```

背後做了

1. 查看 registry
2. 下載東西
3. 執行預設的指令

這樣的作法不會下載任何東西，就很方便

而這個指令在 pnpm 裡面叫做
 
```
pnpm dlx

```