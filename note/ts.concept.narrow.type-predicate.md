# ts.concept.narrow.type-predicate

## type guard

我們常會寫一些 is 判斷式來作使用，例如

```ts
const isHuman = (i: any) => {
    return typeof i.name  === 'string'
}


function print (i: object) {
    if (isHuman(i)) {
        // i = type object
    }
}
```

但在這種情形， if block 內部是不會知道他的 type 是 Human 的。只知道 isHuman 會回傳一個 boolean 而已。

這時候如果有這種 return  boolean 的判斷式，可以附註他是什麼樣型別的斷言

```ts
const isHuman = (i: any): i is Human => {
    return typeof i.name  === 'string'
}


function print (i: object) {
    if (isHuman(i)) {
        // i = type Human
    }
}

```

## this type guard
這件事情同時也可以用在 class 的 method 上面，而且可以用來判斷 this

https://www.typescriptlang.org/docs/handbook/2/classes.html#this-based-type-guards


```ts
class FileSystemObject {
  isFile(): this is FileRep {
    return this instanceof FileRep;
  }
  isDirectory(): this is Directory {
    return this instanceof Directory;
  }
  isNetworked(): this is Networked & this {
    return this.networked;
  }
  constructor(public path: string, private networked: boolean) {}
}
 
class FileRep extends FileSystemObject {
  constructor(path: string, public content: string) {
    super(path, false);
  }
}
 

```