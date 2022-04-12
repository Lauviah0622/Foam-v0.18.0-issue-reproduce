# ts.concept.variance.function


我們如何定義 function 之間的變異性，也就是寬鬆 or 嚴謹的程度。要注意的是，這邊的變異性指的是作為被使用，也可說是作為參數的行別而言的變異性，而不是 function 本身的變異性

在看 function 的變異性，我們看的會是「如果要使用這個 function，我們要怎麼判斷使用這個 function 的時也可以使用另外一個 function」，兩個 function type 之間的行別變異性的比較

function 這個東西可以分成兩個部分來看：input 以及 output。

在 JS 裡面，
input 會是： 參數、this 還有外層 scope 的變數（但閉包在 ts 裡面是不可表示的）
output 會是： return 出來的值

可以從這兩個層面來探討怎麼樣的 function 會是另外一個 function 的子型別

### input

input 這東西是會在 function 內部被呼叫的，我們可以這樣想。如果是同樣的 input，可以被這個 A function 作使用，但不能被 B function 作使用。那我們會說 B function 比較嚴格。舉例

```ts
type person = {
    name: string
    age: number
}

function sayName(p: {name: string}) {
    console.log(p.name)
}

function sayNameAndAge(p: {name: string, age: number}) {
    console.log(p.name, p.age)
}
```

上面這個簡單的例子就可以看到 SayName 的 input 會比 SayNAmeAndAge 的 input 寬鬆。所以我們可以說 SayName 這個 function 比較 「寬鬆」

為什麼？是不是比較寬鬆這件事情說白了就是

> 如果能夠帶入 A 的地方，也能夠帶入 B。但是能帶入 B 的地方，不能一定能代入 A。那就代表著 B 比 A 寬鬆。

```ts
function MaxTalk(say) {
    const Max = {
        name: 'Jack',
    }

    say(me)
}

function JasonTalk(say) {
    const Jason = {
        name: 'Jack',
        age: 12
    }
}

MaxTalk(sayName)
MaxTalk(sayNameAndAge) //Error, me.age not found
JasonTalk(sayName)
JasonTalk(sayNameAndAge)
```
從上面的例子來看，SayName 兩個都可以帶入，但 sayNameAndAge 卻不能帶入 JasonTalk。這就代表著 sayNameAndAge 比 SayName 嚴謹，所以 sayNameAndAge 會是 SayNAme 的子型別

所以我們可以看出來，function 之間，input 比較嚴謹的 function 會是 input 比較寬鬆的 function 的子型別

### return

return 出來的行別是需要被外部被應用的。在對於被應用這回事，我們應該盡可能提供更多的內容，才能夠廣泛的被應用。

```ts
function createPersonData (name: string, age: number) {
    return {
        age,
        name
    }
}

function createWorkerData (name: string, age: number) {
    return {
        age,
        name,
        job: 'worker'
    }
}

function scanMaxDataId(dataCreator) {
    const Max =  {
        name: 'max',
        age: 12,
    }

    const maxData = dataCreator(Max)
    const isMaxHasId = !!maxData.id
}

function scanMaxDataJob(dataCreator) {
    const Max =  {
        name: 'max',
        age: 12,
    }

    const maxData = dataCreator(Max)
    const isMaxHasJob = !!maxData.job
}

scanMaxId(createWorkerData) 
scanMaxId(createPersonData) 
scanMaxDataJob(createWorkerData) 
scanMaxDataJob(createPersonData) // error .job is not defined

```

我們可以比較 createWorkerData 以及 createPersonData 這兩個 function
- createWorkerData，他產生了 `{name: string, age: number, job: string}` 的 type
- createPersonData，他產生了 `{name: string, age: number}` 的 type

createWorkerData 的 return 值本身有更多的屬性供使用，換句話說，從被帶入的角度來看，createPersonData 反而對於可以使用他的 type 限制更大，因為本身提供的屬性比較少，而 createWorkerData 可以提供更多的選項。所以如果 function 的 return 值越嚴謹，反而是比 return 值更寬鬆的 function 更加寬鬆。


上面都是用 type shape 來看。但如果是從非 shape type 的角度來看事情會變得很奇怪。

從 return 值來看

```ts
function createId(id: number):string | number {
    return id > 50 ? id : `${id}`
    
}

function createNumberId(id: number):number {
    return id
}
```

奇怪，從「能提供使用的選擇來看」 createNumberId 只提供了 number 這個選項作使用，但是 createId 可是提供了 string 還有 number 作使用欸。但是 createNumberId => number 本身卻是 createId => string | number 還要嚴謹。

上面的說法：createId 能提供 string 以及 number 作使用這件事情理解錯了。

使用 createNumberId 的 return 值時，我們只需要實作 number 的處理就好了
但是在使用 createId 時，我們卻要實作 string 還有 number 的處理。所以 createId 對於使用他的 function 會是比較嚴格的。而 createNumberId 就只要實作 nubmer 的使用就好了


我們再從 參數來看非 shape type 的使用情境

```ts
function createId(id: number | string) {
    return `${id}`

}

function createNumberId(id: number) {
    return id
}

```

對於參數而言就比較直觀了，使用 createId 時，我們可以接受 createId 的 number 或者 string，而 createNumberId 只能接受 number。這樣看下來我們可以很直觀的知道 createId 實作需要比較嚴格的條件，需要實作 number 的處理以及 string 的處理。

但相對的 createNumberId 就只要處理 number 就好了

所有，可以帶入 createNumberId 的地方都可以帶入 createId，但是可以帶入 createId 的地方卻不一定可以帶入 createNumberId，因為 createNumberId 並沒有實作 string 的部分。


結論：在看 function type 對於型別符不符合所謂的協變性的時候
- 在 input，也就是 this, argument 而言，屬不屬於目標的超型別
- 在 output，也就是 return，要看屬不屬於目標的子型別