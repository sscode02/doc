大家都知道 == 会发生隐式转换, 那具体的转换规则是怎样的呢？
		1. 当对比一方有数字时,另一边时string时，会把string转换为数字
		2. 当对比一方有boolean时,会把true转换为1，false转换为0
		3. 当一方是对象时会调用valueof ,然后在对上面规则进行转换

还有一些其他规则
	null 和undefined相等
	null和undefind不会转换成其他类型进行比较
	任何一方时nan时返回false
	两个对象比较时 会判断是不是引用同一个对象

