# typescript.interface



```ts
type Food1 = {
    calories: number
    salty: boolean
    tasty: boolean
}

interface Food2 {
    calories: number
    salty: boolean
}


interface Cookie extends Food2 {
    sweet: boolean   
}

```

1. type 要等於、interface 不用等於
2. 能夠透過 extends 來建立 upper bound


不過 extends 並不是專屬於 interface 的語法，interface 可以 extends 所有「形狀」，像是 class, object type, interface

```js
interface Cookie2 extends Food1 {
    sweet: boolean   
}
```
1. interface 本身可以作 [[typescript.declaration-merging.md]]

> 覺得 interface 本身就應該在真正需要 interface 的地方作使用。





#toBeClarify
```ts
interface Physic {
    area: string
}


class PhysicTeacher implements Physic{ //Class 'PhysicTeacher' incorrectly implements interface 'Physic'. Property 'area' is protected in type 'PhysicTeacher' but public in type 'Physic'.ts(2420)
    constructor(
        protected area: string,
        name:string,
        age:number,
        subject: string
    ) {
        super(name, age, subject)
    }
}
```

在這樣的情況，如果一個 class implements interface，但是用非 public 的 modifier，像這邊的 protected，這樣會報錯。

https://stackoverflow.com/questions/55504577/i-cant-make-a-class-field-implemented-from-interface-private-nor-make-interfac

根據上面這篇的回答，因為 interface 就如同他的名稱，這是一個接口，既然是 interface，那就必須要暴露給外部才能作使用，所以必須是 public... 覺得有點強詞奪理...


[[ts.extends-abstract-vs-impl-interface]]