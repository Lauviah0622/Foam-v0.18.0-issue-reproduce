# structurally_and_nominally_typed

結構定型structurally typed & 名義定型 nominally typed

structurally typed：從 object 的結構來判斷說這兩個 object 是不是一樣的

JS 本身屬於 structurally typed，例如
```
const obj1 = {
    name: "peter"

}

function Man(name) {
    this.name = name
}
const obj2 = new Man("peter")
// { name: "peter"}


const function Dog(name) {
    this.name = name
}

const obj3 = new Man("peter") 
// { name: "peter"}

```

對 JS 普遍的使用而言（注意，是普遍的使用），雖然這三個東西是不同的製造方式，但是我們會是為同一個東西。我們不管他們怎麼製造或者說變數名稱是什麼樣，我們只管裡面的結構，這個叫做 structurally typed

但是在其他語言，可能即使結構一樣，只要是不同的 constructor，就被視為是不同的物件，就被視為 nominally typed

但是 JS 本身並不是沒辦做到 nominally typed，我們也可以做這樣的檢查

```
obj1.__proto__.constructor.name === obj2.__proto__.constructor.name
// a.__proto__.constructor 可以拿產生他這個 instance 的 function (constructor)，然後 name 可以拿 function 的名稱
```

但是我們通常不會這麼做r，所以才說是普遍的使用

