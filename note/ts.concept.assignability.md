# ts.concept.assignability

A 能不能指定給型別 B

1. 如果 A <: B(B 型別是 A型別的超型別) => 就可以指定給 type B
2. A 是 any

any 雖然是任何型別的超型別，但是卻可以指定給任何 type

