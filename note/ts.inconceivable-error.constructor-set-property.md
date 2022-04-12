# ts.inconceivable-error.constructor-set-property


```ts
class MyMap<K, V> {
  constructor(initKey: K, initValue: V) {
    this[initKey] = initValue;
  }
}

```

就像上面的 code 一樣，我要怎麼做到侷限 props 的型別，然後又讓 initKey 跟 initValue 變成 class 的 property
