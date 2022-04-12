# ts-feature

- gradually-typed：全部不寫也可以是 TS，你可以一點一點慢慢加上型別，不一定要全部加上去才能執行（例如[[type_system]] 裡面提到的的 Java, C），這樣的特性讓 TS 可以直些使用舊的 JS lib
- 可以直接寫 TS，也可以在舊的 JS lib 只要加上型別描述（.d.ts file），雖然不經過 TS compile 檢查，但是依然可以讓 IDE 可以做型別檢查


TS 的主要目的是讓型別錯誤這種問題在編譯時間就被抓出來，看看我們公司的專案到底出現多少次這種錯誤...