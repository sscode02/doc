
当我们creareRouter时,会进行下面操作

1. 根据用户传入的routers 生成一个 matchers 
2.  通过createWebHistoy 监听popstate
3. push 逻辑

1.通过app.component在vue全局挂载routerLink和routerview

2.push到当前的location, 比如 a.com/chdilren  就会执行router.push('/chdilren')

3.会建立一个currentRoute去存储 match到的component，currentRoute 是一个shalowref 对象

4.currentRoute 会被provide 成全局变量 inject 到routerView 组件中 当currentRoute  更改时 routerView 也会变更 

5.routeLink 使用preventDefaut 阻止了默认事件 （a 的跳转）
