1.  创建VNode

```javascript
const vnode = createVNode(rootComponent, tooyProps);
```

2.  渲染VNode
```javascript
render(vnode, rootContainer,isSvg); 
```

render 发生了什么？
	1.判断oldVnode存在 而newVnode 不存在就 unmount 
	2.要不然就patch
	3.根据传入的vnode type 进行不同的挂载

	以component 为例
	如果oldVnode不存在 newVnode存在就mount

4. 创建一个实例instance 
	1. 会加工这个实例
	2. 创建一个副作用函数 并且会创建一个reactive 实例