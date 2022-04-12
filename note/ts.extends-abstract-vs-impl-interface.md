# ts.extends-abstract-vs-impl-interface


直接 extends abstract class vs implements interface

```ts
abstract class Person {
  constructor(public name: string) {}
}

class Teacher extends Person {
  constructor(name: string) {
    super(name);
  }
}

class Teacher2 implements Person {
    constructor(public name: string) {

    }
}
```


1: Teacher 使用 extends abstract class
2: tea cher2 implements Person
- 因為 1. 是 class，所以是有實際上建立一個 object 的，但 2. 沒有，只有 type
- 1. 可以做到比較細緻的控制，像是 property 的 private 之類的， 2. 就一定全部都要 public
- 2. 可以 implements 多個 interface



