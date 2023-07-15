
  ptototype属性是在声明函数时创建的
  而__proto__是每个对象的内部属性 指向其原型
  
  举个例子
```javascript
function Foo() {
	console.log('hello')
	}
	const a = new Foo()
	
	a.__proto === Foo.prototype //true
```

当然除了__proto__ 可以获得其原型外 Object.getPrototypeOf(obj)也可以

当我们创建一个Object时 const a = {}
	a.__proto__指向Object构造器的prototype 也就是 `a.__proto__ === Object.prototype`

让我们思考下面这个例子
```javascript
function Foo(){}
const a = new Function()

Foo.__proto__ == a.__proto__ //true
```

在这里我们可以发现 Foo的__proto__ 指向的是 Function.prototype, 而a.__proto__也指向 Function.prototype 所以在直接声明Foo时 Foo的__proto__ 会指向Function.prototype 就像直接声明一个对象 这个对象的__proto__ 会指向Object.prototype

##### 到这里我们可以总结两个点
1. prototype 是函数独有 并且在作为其构造函数的时候 会把该函数的prototype链接到其实例的__proto__上,这样的好处就是我们可以在函数中实现继承
2. __proto__就相当于获取当前对象原型链的一个入口

题外话 我们在声明一个函数的时候 打印其prototype时 会发现这个对象中只会包含 一个constrcutor 并且这个constrcuor 会指向其函数

```javascript
function Foo() { }
Foo.prototype.constructor === Foo //true

const a = new Foo()
a.constructor === Foo // true
```

在这里 我们会很为这个constructor 这个属性会指向其构造他的函数 但是实际上这个理解是有误的
``` javascript
function Foo() { }
Foo.prototype = {}
const a = new Foo()

a.constructor === Foo //false
a.constructor === Object //false
```
在这个例子中object 并没有构造a, 因为a没有constructor属性 所以会委托其原型链一步步往上找直到发现 Object.prototype 有其constructor 所以在项目中我们应该尽量避免时用其属性 