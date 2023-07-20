
reactiveeffact是vue3 包裹副作用的一个类, 在这个类中解决了副作用嵌套，清理依赖问题
vue在执行副作用的时候会把该类的实例绑定到全局的activeeffact 上从而被收集。依赖所对应的副作用函数其实就是这个类的实例
具体实现方法

```javascript 
let activeEffact 

class RactiveEffact {
	parent 
	constructor(public fn, public scheduler) { }
	run() {
		this.parent = activeEffact 
		activeEffact = this
		this.fn()
		activeEffact = this.parent
		this.parent = undefined
	}
}
```

这里声明需要保证 在收集依赖的过程中 activeEffact 始终要指向当前的实例，但是在收集的过程中activeEffact 可能会被覆盖