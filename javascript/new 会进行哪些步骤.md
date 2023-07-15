```javascript
	function fakeNew(constrcutor,...args){
		const temp = {} // 1. 创建一个临时对象

		temp = Object.setPrototypeOf(temp,constrcutor.prototype)
		// 2. 把该函数的__proto__ 指向该函数的prototype


		//3. 把该临时对象绑定到 该构造函数上
		constrcutor.call(temp)
		
		// 4. 如果该构造函数有返回值 并且返回的是对象 就直接返回 原始值就返回创建的临时变量
		return temp	
	}
```