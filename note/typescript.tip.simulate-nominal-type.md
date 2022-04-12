# typescript.tip.simulate-nominal-type

有題到 JS 還有 TS 基本上都是結構定型 [[structurally_and_nominally_typed]]

但有時候可能會需要名義定型會比較方便，例如就像我們公司會有 promoID, prizeID, lotteryId 一狗票 Id，每個 id 只能用在特定的是地方


不過我們可以透過一些卑鄙小技巧來做到結構定型


```ts
type PromoId = string & {readonly tag: unique symbol}
type LotteryId = string & {readonly tag: unique symbol}
type UserId = string & {readonly tag: unique symbol}


let a1:PromoId = 'promoID123'; //宣告 a 的行別為 PromoID 會報錯
let a2 = 'promoID123' as PromoId; // 只能用斷言賦予

function createPromoId(id: string){
    return id as PromoId
}

function printPromoId(id: PromoId) {
    console.log(id);
}

let id = createPromoId('123123') //雖然 function 本身沒有意義（就是直接回傳），但是可以建立型別

printPromoId(id) // 如此一來就可以安全的使用

```