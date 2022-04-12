# ts.concept.type-widening.freshness

TS 在單單處理「值」時一樣會幫你推斷型別，但這時候推斷出來的型別會帶有 freshness，
而對於有 freshness 的型別，會執行 excess property checking （超量屬性檢查），會特別檢查有沒有「不屬於目標 type 的屬性」

但是如果有使用 assertion，那會破會這個 freshness (或者換個角度想，斷言就不是推斷了，所以沒有 freshness)，所以就不會進行 excess property checking


```ts
type Options = {
    baseUrl: string
    method?: string
    tier?: 'prod' | 'dev'
}

function create(op: Options) {
    return op
}

create({
    baseUrl: '123',
    tirr: 'prod'
}) 
// 只處理值而沒有變數，會對變數進行推斷型別 => 帶有freshness => 進行 excess property checking
// 發現 tirr 是多出來的屬性，所以報錯


create({
    baseUrl: '123',
    tirr: 'prod'
} as Options)

// assertion 沒有進行推斷，所以不報錯

let obj = {
    baseUrl: '123',
    tirr: 'prod'
}

create(obj)
// 非值，而是帶入變數的行別 {baseUrl:string, tirr:string}，而這裡的 op 參數雖然為 Options，但是具有協變性 covariance，所以可以接受比他寬鬆的 type。{baseUrl:string, tirr:string} 因為 tirr 本身 op 參數不管，所以 { baseUrl:string } 檢查通過



```