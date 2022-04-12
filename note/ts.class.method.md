# ts.class.method



### return this

```js
class Set {
    protected props:any[] = []
    has(item:unknown) {
        return this.props.includes(item)
    }

    add(item:unknown):this {
        if (!this.has(item)) {
            this.props.push(item)
        }
        return this
    }
}

```

這個大概只有比較準確的標記說這個 add 的 method 會 returny 自身，而不是