 history 拥有两个事件 pushState 和 replaceState
 pushState会往history栈添加一条页面数据

```js
	// 如果当前在 a.com/a.html
	history.pushState({},'title','b.html')
	//执行后 url 会变成a.com/b.html 这个操作并不会重新请求b.html

```

repalceState 
	会更改当前页的history 信息,使用方法了pushstate一致

history.onpopstate

调用 `history.pushState()` 或者 `history.replaceState()` 不会触发 `popstate` 事件。`popstate` 事件只会在浏览器某些行为下触发，比如点击后退按钮（或者在 JavaScript 中调用 `history.back()` 方法）。即，在同一文档的两个历史记录条目之间导航会触发该事件。

`popstate` 事件的 `state` 属性包含了这个历史记录条目的 `state` 对象的一个拷贝。
```js
 window.onpopsate=(e)=>{
	 e.state 
 }
```