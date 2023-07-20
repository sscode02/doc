在vue3设计reactive 的时候，添加了一个调度器选项，在运行副作用的时候 如果用户传入了scheduler 那么不会立即执行 该副作用，会把执行时机交给用户,computed正是借助shceduler实现的

```javascript
	if(effect.scheduler){
		effect.scheduler()
	}else {
		effect.run()
	}
```

我们现在从computed的使用来看,在这里computed 会返回一个值 当a或b发生变化时 会使sum也发生变化 如果 a和b都没有发生变化时 会返回上一次执行的结果

```javascript
let a = b =1
const sum = computed(()=> a + b) 
```

那我们现在来实现基础功能, 当我们get sum这个值的时候可以拿到 a+b的结果

```javascript 
function computed(fn) {
	const obj = {
		get value() {
		return  effact.run()
		}
	}
	return obj
}
```

在上面的例子中我们每一次get sum.value 的时候都会拿到最新的值,为了添加缓存我们需要添加一个变量，并且在依赖变化时能通知sum,所以我们手动收集创建obj，并且在依赖的时候通知sum

```javascript 
function computed(fn) {
	let dirty = true
	let value // 缓存变量
	
	const effact = new ReactiveEffact(fn, ()=>{
		dirty = true 
		trigger(obj,key) 
	}) // 这个函数就是scheduler，使用箭头函数是为了正确绑定this
	const obj = {
		get value() {
		if(dirty){
			dirty = false
			value =  effact.run()
		}
		track(obj, value) // 手动收集依赖
		ret
	}
	return obj
}
```


``