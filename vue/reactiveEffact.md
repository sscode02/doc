
reactiveeffect是vue3 包裹副作用的一个类, 在这个类中解决了副作用嵌套，清理依赖问题
vue在执行副作用的时候会把该类的实例绑定到全局的activeeffect 上从而被收集。依赖所对应的副作用函数其实就是这个类的实例
具体实现方法

```javascript 
let activeEffect 

class RactiveEffect {
	parent 
	constructor(public fn, public scheduler) { }
	run() {
		try{ // 使用try finally 确保执行return 副作用的时候能运行后面的逻辑
			this.parent = activeEffect 
			activeEffect = this
			return this.fn()
		} finally {
			activeEffect = this.parent
			this.parent = undefined
		}
	}
}
```

这里声明需要保证 在收集依赖的过程中 activeEffect 始终要指向当前的实例，但是在收集的过程中activeEffect 可能会被覆盖 ,所以需要一个变量保存调用当前副作用的副作用。
因为当前activeEffect会被依赖收集函数当作副作用收集，当发生副作用嵌套的时候activeEffect 会被覆盖

举个简单的例子，当我们get 响应式对象的时候 会触发track进行副作用收集 当我们set响应式对象的时候会触发trigger 执行副作用，其实副作用函数就是包裹了render函数
```javascript
const dep = new Set()

function track() {
	if (!activeEffect) return

	dep.add(activeEffect) // 副作用收集
}

function trigger() {
	dep.forEach(effact => effect.run()) //副作用执行
}
```