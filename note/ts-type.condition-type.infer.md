# ts-type.condition-type.infer 


先觀察一下這段語法，然後在講結論


```ts
type Flatten<T> = T extends (infer U )[] ? U : T;

type G = Flatten<['1', '2', '3']>
type G2 = Flatten<'1' | '2' | '3'>
```

如果 T 不符合 (infer U)[] 的形狀，就直接 return T 的型別
如果 T 符合 (infer U)[] 的形狀，就幫你從 T 推斷出 U，然後 return U 的型別


infer 這個東西就是可以你可以設定一個形狀，然後可以他就可以幫你推斷，有點像是 [[ts.generic#呼叫榜定]] 的推斷概念，這個 infer 會在 Alias type 被使用而且符合的時候 才會被推斷


此外還可以作很多有趣的事情

### 限制 infer 的型別

```ts
type Flatten<T> = T extends (infer U & string )[] ? U : T;

type G = Flatten<['1', '2', '3']> // '1' | '2' | '3'
type G2 = Flatten<'1' & '2' & '3'> // never
type G3 = Flatten<[1, 2 ,3]> // [1, 2, 3]
```

1. 如果 T 不符合 (infer U & string)[] 的形狀（至少要是 string 的 array），就直接 return T 的型別，也就是原本輸入的型別
2. 如果 T 符合 ，就幫你從 T 推斷出 U，然後 return U 的型別

### infer 搭配 infer

infer 是可以巢狀的

```ts

type Test<T> = T extends (infer U extends string | number ? true : false)
  ? U
  : T;
```
上面那個沒意義，但下面這個有意義

　```ts
type LastArrayElement<ValueType extends readonly unknown[]> =
	ValueType extends [infer ElementType]
		? ElementType
		: ValueType extends [infer _, ...infer Tail]
			? LastArrayElement<Tail>
			: never;

```

這個很屌

1. LastArrayElement 這個的參數，也就是 `ValueType` 要符合 readonly unknown[]，基本上就是 array
2. `ValueType extends [infer ElementType]` 這是一個 condition，也就是 `[element]` 只有一個東西的 array，如果符合這個 condition，就推斷出 ElementType，並且 return `? ElementType`
3. 如果不符合的話，就進到下一個 condition `ValueType extends [infer _, ...infer Tail]` ，這是多個東西的 array，如果符合的話，會推斷出 `_` array 第一個元素這個的型別以及 `Tail` 剩餘的 array 型別，並且 return `LastArrayElement<Tail>`，也就是把 `Tail` 剩餘的 array 再丟進去 LastArrayElement 再次判定，經過 scheme 摧殘的自己這樣簡單的遞迴簡直不用錢
4. 如果不符合 condition `ValueType extends [infer _, ...infer Tail]` 的話，代表 1. 不符合只有一個 element，2. 也不符合多個 element，那就只剩下空陣列，所以回傳 never







