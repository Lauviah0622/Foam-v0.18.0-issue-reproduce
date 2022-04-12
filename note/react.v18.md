
[[note/react.v18.source.md]]

## TOC 
- Concurrent Mode
    -   

- suspense
- concurrent api
- useExternalStore

## newRootAPI

[[note/react.v18.newRootAPI.md]]



## New Hooks

### useId

方便從資料建立獨一無二的 ID，然後可以在 server side 還有 client side 保持一致

https://reactjs.org/blog/2022/03/29/react-v18.html#useid

> 文件有說不要把這個用在 component 的 key

### useTransition

決定說新的狀態能不能暫停之前的 render，可以更快的看到最新的狀態效果，而且不會被前面 stale state 的 render UI Block 到

### useDeferredValue
有點像 Debouncer?? 感覺是可以延遲某些特定 state 導致的 render，這望不是跟 useTransition 重複？
還是說一個針對 setState，另一個針對 UI


### useSyncExternalStore
> 這個 hook 是只建議給 lib 使用的

目前看不懂，但是跟 subscribe 外部資料有關係
### useInsertionEffect
> 這個 hook 是只建議給 lib 使用的

這個主要是給 CSS-in-js lib 用的。這個 effect 會在 useLayoutEffect 之前，所以現在應該會是

1. reconcile
1. mutate reactDOM
2. useInsertionEffect
3. useLAyoutEffect
4. modify DOM
5. useEffect
