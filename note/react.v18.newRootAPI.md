# react.v18.newRootAPI

之前的用法是這樣

```js

const container = document.getElementById('app');

// Initial render.
ReactDOM.render(<App tab="home" />, container);
```

這樣一來，Component 就會被 render 到 container 這個 element 裡面

現在的用法是這樣

```js
import * as ReactDOMClient from 'react-dom/client';
import App from 'App';

const container = document.getElementById('app');

// Create a root.
const root = ReactDOMClient.createRoot(container);

// Initial render: Render an element to the root.
root.render(<App tab="home" />);

// During an update, there's no need to pass the container again.
root.render(<App tab="profile" />);
```

看起來用法是有點像物件導向的感覺。只要指定一次 root 之後，之後 render 就不用在設定 root 了





