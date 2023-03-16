# bing-countup

[![github]](https://github.com/BingBuLiang/bing-math)  

[uni-app 地址]()

一个轻量级数学渲染 

### 特别说明

出发点：找一个渲染数学公式的组件，虽然uni-app插件市场也有几个，但是不是很如意

使用MathJax，链接： [MathJax | Beautiful math in all browsers.](https://www.mathjax.org/)

配置参考 https://www.osgeo.cn/mathjax/options/menu.html#menu-options

使用uni-app的renderjs，对数学公式（LaTeX）渲染，注：自己写的公式测试时，注意转义符`\`

[在线LaTeX公式编辑器-编辑器 (latexlive.com)](https://www.latexlive.com/)

> 注意: !!!!!!!
>
> 在manifest.json选择vue版本，
>
> 在**vue2**下，该组件可以在浏览器下**正常显示**，手机上也可以**正常显示**
> 在**vue3**下，组件在浏览器**显示不出来**，手机上**正常显示**
>
> 原因：在vue3下，renderjs被初始化加载3次，而vue2下加载2次，
>
> 秉着在手机下能用的态度，啊！啊！啊！目前是不修动了
> 或者你选择Vue2,都可以正常显示，
> 或者选择Vue3,但是在浏览器显示不出来

> 注意2：
>
> 在实例代码下，放了加载用到的js文件，如果想使用本地文件加载，根据注释修改 script.src 即可，
> 默认采用CDN  即：  script.src = 'https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js' 

### 安装方式

本组件符合[easycom](https://uniapp.dcloud.io/collocation/pages?id=easycom)规范，`HBuilderX 2.5.5`起，只需将本组件导入项目，在页面`template`中即可直接使用，无需在页面中`import`和注册`components`。

### 示例

在 ``template`` 中使用组件

```vue
<template>
	<view class="content">
       	<!-- 表达式1 -->
		<view class="show1">
			<bing-math :latex="mathlab1" ></bing-math>
		</view>
        
  		<!-- 表达式2 -->
		<view class="show2">
			<bing-math :latex="mathlab2"></bing-math>
		</view>

		<view class="btn">
			<button @click="update1">修改表达式1</button>
			<button @click="update2">修改表达式2</button>
			<button @click="update3">全部修改</button>
			<button @click="clear">清空</button>
		</view>
	</view>
</template>

<script>
	export default {

		data() {
			return {
				mathlab: '设$f(u)$可导,$z=xy f({y \\over x})$,若$x\\dfrac{\\partial z}{\\partial x}+y\\dfrac{\\partial z}{\\partial y}=xy(lnx-lny)$,则( )',
				mathlab1: '$$x = {-b \\pm \\sqrt{b^2-4ac} \\over 2a \\in} .$$',
				mathlab2: '$$x = {-b \\pm \\sqrt{b^2-4ac} \\over 2a \\in} .$$',
			}
		},
		methods: {
			update1: function() {
				this.mathlab1 += "$dt$"
			},
			update2: function() {
				this.mathlab2 = "$\\Delta X$"
			},
			
			update3: function() {
				this.mathlab2 = this.mathlab
				this.mathlab1 = this.mathlab
			},
			clear:function(){
				this.mathlab1=""
				this.mathlab2=""
			}
		}
	}
</script>

<style>
	
</style>

```
#### 如果需要引用，可以使用以下方式
```javascript
<script>
	import BingMath from "@/components/bing-math/bing-math.vue"
	export default {
		components: {
			'bing-math': BingMath
		}
    }
</script>
```
> **注：** 为确认是否启用bing-math组件及事件，默认有一些console.log()提示，如果不需要提示，可以打开bing-math.vue把所有的console.log()提示信息都删了。



## API

### bing-math @property

| 属性名 | 类型   | 默认值 | 说明            |
| ------ | ------ | ------ | --------------- |
| latex  | String | ' '    | 含有LaTeX的文本 |

​                                                      

## 更新

> 如果大家对兼容有好的方案，请不吝赐教，做好兼容问题