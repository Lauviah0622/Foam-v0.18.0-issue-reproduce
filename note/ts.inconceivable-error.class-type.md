# ts.inconceivable-error.class-type


[[ts.class.type.md]]

到底 class type 是 instance 還是 constructor

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

