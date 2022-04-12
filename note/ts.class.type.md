# ts.class.type

class 關鍵字在 ts 本身除了宣告一個值（也就是一個 instance constructor），同時也宣告一個 type ([[ts.concept.declaration]])

這個 type 並不表示 class 的 本身，而是代表著 class 所建立出來的 instance

好，理論上是這樣，但是有個很怪的現象

```ts
class Person {
  constructor(
    public name: string,
  ) {}
}

const a:Person = new Person('123');

const creator:typeof Person = Person;

const creator2:Person = Person; // 三小？沒報錯？
```