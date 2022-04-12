### interface in class

[[ts.class | class]] 關鍵字本身就具備了宣告還有建立值的功能，除了用 extends 擴充另一個 class，這代表不只型別，也繼承了值。
但如果只想要單純「擴充」一個行別，可以只使用 implements

```ts
abstract class Person {
  constructor(public name: string) {}
}


type PE = {
    goodAr: string
}


class Teacher2 implements Person, PE {
    constructor(public name: string, public goodAr: string) {

    }
}
```

implements 本身不只可以 implements interface，也可以 implements type(基本上就是 type of shape)，而且可以 implements 多個 type/ implement
