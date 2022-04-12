# react.batchUpdate


## v.18

自己寫的文章

https://lavi-blog.vercel.app/posts/react-batch-update/


稍微研究 18.0 之後發現幾個有趣的例子

- batch Update 是以 一次 render 為單位，所以即使有多個 useEffect，並把 setState 放在多個 effect 裡面，也會被 batch

```js
import { useState, useLayoutEffect, useEffect } from "react";
import * as ReactDOM from "react-dom";

function App() {
  const [count, setCount] = useState(0);
  const [count2, setCount2] = useState(0);
  const [flag, setFlag] = useState(false);

  function handleClick() {
    console.log("=== click ===");
    fetchSomething().then(() => {
      // React 18 with createRoot batches these:
      setCount((c) => c + 1); // Does not re-render yet
      setFlag((f) => !f); // Does not re-render yet
      // React will only re-render once at the end (that's batching!)
    });
  }

  useEffect(() => {
    setFlag((f) => !f);
  }, [count]);

  useEffect(() => {
    setCount2((s) => s + 1);
  }, [count]);

  return (
    <div>
      <button onClick={handleClick}>Next</button>
      <h1 style={{ color: flag ? "blue" : "red" }}>{count}</h1>
      <h1 style={{ color: flag ? "blue" : "red" }}>{count2}</h1>
      <LogEvents p={{count, count2, flag}}/>
    </div>
  );
}

function LogEvents({p}) {
  useLayoutEffect(() => {
    console.log("Commit", p);
  });
  console.log("Render", p);
  return null;
}

function fetchSomething() {
  return new Promise((resolve) => setTimeout(resolve, 100));
}

const rootElement = document.getElementById("root");
// This opts into the new behavior!
ReactDOM.createRoot(rootElement).render(<App />);

```

```
=== click === 
Render 
{count: 1, count2: 1, flag: false}
Commit 
{count: 1, count2: 1, flag: false}


Render 
{count: 1, count2: 2, flag: true}
Commit 
{count: 1, count2: 2, flag: true}

```