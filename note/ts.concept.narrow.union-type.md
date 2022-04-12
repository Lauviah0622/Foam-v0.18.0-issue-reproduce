# ts.concept.narrow.union-type

假設有這樣的情境


有兩個 Event 的 union type 作為參數，然後我們需要在 function 中 narrow 他們

```ts

type UserTextEvent = {v: string, target: HTMLInputElement}
type UserMouseEvent = {v: [number, number], target: HTMLElement}
type UserEvent = UserTextEvent | UserMouseEvent

function handle(e:UserEvent) {
    if (e.v === string) {
        console.log(e.v);
        console.log(e.target);
    }
    console.log(e.v);
    console.log(e.target);
    
}
```

雖然在 在 JS 中，我們可以很清楚知道 if 內部就一定是 UserTextEvent，但是 TS 沒有那麼聰明。兩個不同的 Event 經過 Union 之後型別全部混在一起，會變成這樣

```ts
type UserTextEvent = {v: string, target: HTMLInputElement}
type UserMouseEvent = {v: [number, number], target: HTMLElement}
type UserEvent = UserTextEvent | UserMouseEvent

/**
 type UserEvent = {
     v: string | [number, number]
     target: HTMLInputElement | HTMLElement
 }
 */
```

這會讓我們在 narrow 的時候沒辦法 narrow 出特定的型別。要在 union type 中 narrow 出特定的型別，必須要

1. 在被 Union 的所有 type 都加上提供辨識的 Tag Property
2. Tag Property 的行別必須是 literal type，也就是確切的行別，像是 1, 2, 'type1', true, false 等等