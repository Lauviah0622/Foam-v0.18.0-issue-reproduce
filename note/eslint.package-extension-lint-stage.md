# eslint.package-extension-lint-stage

eslint 在設定的時候，會有三個跑的時機

1. 直接使用 package
2. estension 的 check
3. lint-stage


這三個東西吃到的設定值，非常有可能不一樣

例如 extension 有時候就會吃不到 mono-repo 引入的設定值，就會導致使用 eslint package 不會報錯，但是 extension 會有紅色毛毛蟲