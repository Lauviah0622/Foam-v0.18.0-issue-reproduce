# ts-type

![[ts-type-hierarchy]]

## TS type
### any
所有型別的聯集

使用情境
非常的「不要」出現這個東西

[[tsconfig-setting#noImplicitAny|設定 type inference 的 any 會報錯]]
[[ts-type-any]]
### unknown

使用情境
在真的不知道這個值的來源會是什麼的時候

[[ts-type-unknown]]
### boolean 
[[ts-type-boolean]]

### number
[[ts-type-nubmer]]

### bigint
[[ts-type-bigint]]

### string
沒啥好講的
和 boolean, number 等等 primitive value 一樣，同樣可以用 [[type-literal]]

### symbol
[[ts-type-symbol]]

### object
[[ts-type-object]]

### Array

[[ts.type-array.md]]


### tuple

[[ts.type-tuple.md]]

### absence type 

就是空空的型別，包含了 null, undefined, void, never

[[ts.type-absence.md]]

### enum

[[ts-type-enum.md]]


## type operator
[[ts-type.operator.md]]


就是怎麼樣去操作 type 

## Conditional Types

[[ts-type.condition-type.md]]

## assertion

[[ts-type.assertion.md]]