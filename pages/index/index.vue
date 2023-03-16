<template>
	<view class="content">
		<view class="show1">
			<bing-math :latex="mathlab1" ></bing-math>
		</view>

		<view class="show2">
			<bing-math :latex="mathlab2"></bing-math>
		</view>

		<view class="btn">
			<button @click="update1">修改表达式1</button>
			<button @click="update2">修改表达式2</button>
			<button @click="update3">全部修改</button>
		</view>
	</view>
</template>

<script>
	export default {

		data() {
			return {
				// mathlab: '$$x = {-b \\pm \\sqrt{b^2-4ac} \\over 2a \\in} .$$',
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
			}
		}
	}
</script>



<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.math {
		height: 150rpx;
		width: 100%;
	}
</style>
