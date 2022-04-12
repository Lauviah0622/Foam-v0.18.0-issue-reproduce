# ts.concept.totality



周延性，表示型別中所有的 case 都需要符合 function return value 

```ts
type Weekday = 'Mon' | 'Tue' | 'Wed';

function getNextDay(w: Weekday):Weekday { //Function lacks ending return statement and return type does not include 'undefined'.ts(2366)
    switch (w) {
        case 'Mon':
            return 'Tue'
    // 如果不符合 'Mon' 就沒有 return 值了，不符合 (Weekday) => Weekday
    }
}

```

所以需要加上

```ts
function getNextDay(w: Weekday):Weekday | undefined{ 
    switch (w) {
        case 'Mon':
        
            return 'Tue'
    
    }
}
```

或者是

```ts
function getNextDay(w: Weekday):Weekday { 
    switch (w) {
        case 'Mon':
            return 'Tue'
        default 
            return 'Tue'
            // 總而言之要有一個 defualt 符合
    }
}
```


### 不指定 return type 的完備性檢查

如果要檢查，必須要開啟 [[tsconfig-setting#noImplicitReturns]]。開啟了這個，會檢查是不是所有的 pattern 都有 return 值。如果是的話才會通過，不是則不會通過


```ts
function isBig(n:number) { // warning: Not all code paths return a value.ts(7030)
    if (n >= 100 ) {
        return true
    }
 
}
```



