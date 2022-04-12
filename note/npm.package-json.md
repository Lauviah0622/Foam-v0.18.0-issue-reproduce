

### files

表示說如果這個 專案作為 dependency 下載時，包含哪些檔案。

如果沒有設定，預設就是整個專案所有的檔案，除了：

```
.git
CVS
.svn
.hg
.lock-wscript
.wafpickle-N
.*.swp
.DS_Store
._*
npm-debug.log
.npmrc
node_modules
config.gypi
*.orig
package-lock.json

```

package-lock.json 比較特別，我們都知道他是用來固定 dependecies 的 dependency 的版本的，但如果要作 publish，應該要用  npm-shrinkwrap.json 這個檔案

如果有設定這個東西，那在使用 npm publish 的時候就只會打包 files 中列出的檔案。我們也可以用 npm pack 這個試打包看看。


https://stackoverflow.com/questions/40795836/how-do-you-use-the-files-and-directories-properties-in-package-json

這個回答有更詳細的介紹