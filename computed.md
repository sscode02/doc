在设计reactive 的时候我们添加了 scheduler（调度器）

```javascript
effactToRun.forEach((effact: any) => {
	if (effact?.options?.scheduler) {
		effact.options.scheduler(effact) //这里不会立即执行副作用
	} else {
		effact()
	}
})
```

我们现在从computed的使用来看,在这里computed 会返回一个值 当a或b发生变化时 会使sum也发生变化 如果 a和b都没有发生变化时 会返回上一次执行的结果

```javascript
let a = b =1
const sum = computed(()=> a + b) 
```

那我们现在来实现computed 