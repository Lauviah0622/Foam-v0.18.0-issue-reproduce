# ts.class.property-modifier

ts 中可以用這樣的語法，直接把 constructor 的參數榜定進去 this

```ts
class ClassName {
    constructor (
        props1: Prop1, // 不榜定
        private props2: Prop2, // 直接榜定進去 this. 而且外界看不到
        private props3: Prop3,

    ) {

    }
}

```

規則是這樣：

只要有用 修飾符的 constructor 參數，就會直接被綁定進去 class 的 this 裡面，包含

- public (default) 
- private
- readonly
- static
- protected


### private
private 的東西只有 class 裡面看得到，使用的時候不用先在 class 內部宣告

> #toBeClarify  
> 那如果被繼承的元素可以使用嗎？ => 不行，只有自己才看得到


此外，如果自己的 method 裡面想要存取自己 instance 的 private property 也是允許的
```ts

class Position {
  constructor(private file: Files, private rank: Rank) {}

  distanceFrom(position:Position) { //使用以自己 class 的 instance
    return {
            rank: Math.abs(position.rank - this.rank), // 一樣可以直接存取 position.rank
            file: Math.abs(position.file.charCodeAt(0) - this.file.charCodeAt(0))
        }
    }
}
```


### protected

被繼承的元素可以使用，使用的時候需要在 class 內部先宣告 property，像是這樣

```ts
class Piece {
    protected position: Position // 先進行宣告
    constructor(
        private readonly color: Color,
        public name: string,
        file: Files,
        rank: Rank
    ) {
        this.position = new Position(file, rank); // 後面在進行賦值
    }

}
```

在這邊同時開啟 [[tsconfig-setting#strictNullChecks]] 以及 [[tsconfig-setting#strictPropertyInitialization]]，會檢查上面的 position 有沒有被賦值


### abstract 
有兩種用法：
1. 可以在 class 前面使用，如果使用的話，那這個 class 就不能直接被 new，只能被 extends

```ts
abstract class Piece {
    //...
}

new Piece() //error，因為 abstract 的 class 不能直接建立 instance

```

2. 可以在 class 中的 method 或者屬性使用

```ts
class Piece {
    abstract go(x: number, y:number):void // 並不是真的 method，而是規定一定要實作
}

class King extends Piece { 
    go(x:number, y:number) { //一定要實作這個 method 不然就會報錯
        this.x = x;
        this.y = y;
    }
}
```

[[ts.extends-abstract-vs-impl-interface.md]]


