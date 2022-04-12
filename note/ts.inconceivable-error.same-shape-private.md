# ts.inconceivable-error.same-shape-private

```ts
class A {
    private x = 1
}

class B extends A {}

function f(a: A) {
    console.log(a);
}

class C {
    private x = 1
}

f(new A)
f(new B)
f(new C) // Argument of type 'C' is not assignable to parameter of type 'A'. Types have separate declarations of a private property 'x'.ts(2345)
```

超怪= =，如果上面的 A.x 沒有 private 那就不會有這個錯誤

在 P.106 是有提到，但這個例子即使 C 也是 private，也會報錯

