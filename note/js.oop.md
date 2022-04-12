# JS OOP



### super method

super 本身的功用是呼叫自己 extends 的對象（稱作 parent）的 function


```js
class Animal {
    constructor(name) {
        this.name = name
    }

    species = 'animal'

    say() {
        console.log(this.name);
        console.log(this.species);
    }
}

class Dog extends Animal {
    constructor(name) {
        super(name) // 調用 parent 的 constructor，只能在 construtor 裡面使用
    }

    say() {
        console.log('i"m dg');
    }

    species =  'Dog'

    woof() {
        this.say(); // 調用自己的
        super.say(); // 調用父層的，但是相當於把 this 綁定到自己身上
        
    }
}

let d = new Dog('Jak')
//i"m dg
// gogo
// Dog
d.woof()

```