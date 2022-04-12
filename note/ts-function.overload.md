# ts-function.overload

```ts
type Log = {
  (m: string, id: number): void;
  (m: string, id: string): void;
};

const log: Log = (m, id) => {
  if (typeof id === "number") {
    console.log(m, id + 1);
  } else if (typeof id === "string") {
    console.log(m, `${id}_1`);
  }
};

```

可以利用 overload 來建立符合多種特徵的 function 

例如上面的 log，就必須同時能夠處理 id 為 number 以及 string 形式


宣告形式的 overload

```ts
function log(m: string, id: number):void
function log(m: string, id: string):void{
    //...
}
```

或者是書上的範例，為 createElement 加上型別

```ts
function createElement(tag: 'a'):HTMLAnchorElement
function createElement(tag: 'canvas'):HTMLCanvasElement
function createElement(tag: 'table'):HTMLTableElement
function createElement(tag: string):HTMLElement {
    //.
}
```

上面這樣宣告的意義在於， TS 會知道是哪一種狀況，這樣你之後就可以直接用對應的 ittelisence 或者是 function 



除了直接宣告外，function over load 也可以用在 object 內部

```ts
type ShoeFactory = {
  create: {
    (type: 'boots'):Boots
    (type: 'cc'):CC
    (type: 'sneaker'):Sneaker
  }
}

```

或者是

```ts
type ShoeCreator = {
  create(type: 'balletFlat'): BalletFlat
  create(type: 'boot'): Boot
  create(type: 'sneaker'): Sneaker
}
```
