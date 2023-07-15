##### 什么是bfc bfc有什么用
	把bfc看作独立的渲染区域 它有自己的渲染规则 如果拥有了bfc bfc里的内容不会影响到外面的布局

1. 避免外边距重叠
2. 清除浮动
3. 阻止元素被浮动元素覆盖

#### 如何触发bfc
	display:flow-root
	overflow:
	position: absolute fixed

浏览器默认排列
普通流
浮动
据对定位
