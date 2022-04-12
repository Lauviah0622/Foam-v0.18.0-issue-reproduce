# ts-type.operator.keying-in



可以直接指定 [[ts.concept.shape-type]] 屬性的行別，就像選擇 object 的 key 一樣

```ts
type APIresponse = {
    user: {
        userId: string
        friendList: {
            count: number,
            friends: {
                firstName: string,
                lastName: string
            }[]
        }
    }
};

const list:APIresponse['user']['friendList']

```


### array 的 keying-in

如果是在 array 上可以用特別的關鍵字 number，這樣就可以遍歷整個 array 的 element 的行別

```ts
type EType<T extends unknown[]>  = T[number];

type K = EType<['123', true, 123]>
```