# ts-function.generic

行內語法

### function 的 generic

直接在 arrow function 前面宣告 type

```ts
const map = <T>(arr: T[], f: (e: T) => any): T[] => {
  const newArr = [];
  for (let i = 0; i < arr.length; i++) {
    const e = arr[i];
    newArr.push(f(e));
  }
  return newArr;
};

```


function 
```ts
function filter<T>(arr:T[], f: (e:T)=> boolean):T[] {
  const newArr:T[] = [];
  for (const e of arr) {
    if (f(e)) {
      newArr.push(e);
    }
  }
  return newArr;
}
```

完整個

```ts
type Filter {
  <T>(arr:T[], f: (e:T) => boolean):T[]
}
```

#### 呼叫榜定
type 會再 function 被 call 的時候，依照 argumnet被綁定


ex:

```ts
// 這個時候是未知
function filter<T>(arr:T[], f: (e:T)=> boolean) {
  //...
}

filter([true, false, true])// 這個時候才知道T 式 boolean
```
##### 指定呼叫時的泛型
除此之外我們也可以在呼叫的時候指定泛型

```ts
filter<boolean>([true, false, true])
```

這樣就換成限制 argument 的 型別，如果是

```ts
filter<boolean>([1, 2, 3]) //Argument of type 'number[]' is not assignable to parameter of type boolean[]'.  Type 'number' is not assignable to type 'string'.
```


### alias generic

這東西何上面的 [[#function 的 generic]] 很像，but 有個很不一樣的東西是
這個的 type 是一個型別的變數，而不是像 function 一樣是在 function 被執行的時候依照 argument 被判定的

```ts
type Filter<T> =  (arr: T[], f: (e:T) => boolean) => T[]

const filt:Filter<number> = (arr, f) => {
  //...
}
```

完整的形式

```ts
type Filter<T> = {
  (arr: T[], f: (e:T) => boolean):T[]
}
```

type 的 generic 就樣 type 的 function 一樣，需要輸入型別的參數來使用，所以也像 function 一樣，可以有輸入預設參數

```ts
type Filter<T = string> = {
  (arr: T[], f: (e:T) => boolean):T[]
}

```
像這樣就沒有必要一定要設定一個參數給他

此外， type alias genetic 也可以使用 [[ts-type.operator.extends]]








### object generic

