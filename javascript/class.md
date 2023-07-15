使用 new 创建实例的时候 construct 也会 经过 new的四个步骤
```javascript
	class Foo {
		constructor(){}
		geta(){} // geta 在Foo.prototype上
	}

const instance = new Foo()

instance.__proto__ = Foo.prototype
```