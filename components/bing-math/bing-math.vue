<template>
	<view class="content">
		<view v-html="mathlab" :mathlab="mathlab" :change:mathlab="math.receiveLab" class="latexId">
		</view>
	</view>
</template>

<script>
	export default {
		name: "bing-math",
		props: {
			latex: {
				type: String,
				default: ''
			},
		},
		data() {
			return {
				mathlab: ''
			}
		},

		watch: { // 监视latex的变化
			latex: {
				handler(newval, oldval) {
					/* console.log("oldval", oldval);
					console.log("newval", newval); */
					this.mathlab = newval;
					this.$forceUpdate();
				},
				deep: true
			}
		},
		mounted() {
			this.mathlab = this.latex;
		}
	}
</script>

<script module="math" lang="renderjs">
	export default {

		methods: {
			// 接收逻辑层发送的数据
			receiveLab(newValue, oldValue, ownerVm, vm) {
				console.log("newValue", newValue);
				this.mathlab = newValue;
				if (typeof window.MathJax != 'object') {
					console.log("window.MathJax", window.MathJax);
					this.initMathJax();
				}

				// 根据id渲染重新渲染
				const el = document.getElementsByClassName('latexId');
				this.renderByMathjax(el)
			},

			initMathJax() {
				window.MathJax = {
					tex: {
						inlineMath: [
							['$', '$'],
							['\\(', '\\)']
						], //行内公式选择符

						displayMath: [
							["$$", "$$"],
							["\\[", "\\]"]
						], //段内公式选择符
						// 支持渲染某些公式
						processEnvironments: true,
						processRefs: true,
					},
					// 参考官方文档 https://www.osgeo.cn/mathjax/options/menu.html#menu-options
					options: {
						//关闭右击选择菜单
						enableMenu: false,
						// 跳过渲染的标签
						skipHtmlTags: ['noscript', 'style', 'textarea', 'pre', 'code', 'a'],
						// 跳过mathjax处理的元素的类名，任何元素指定一个类 tex2jax_ignore 将被跳过，多个累=类名'class1|class2'
						ignoreHtmlClass: 'tex2jax_ignore',
					},

					svg: {
						scale: 1.2
					}
				};
				(function() {
					var script = document.createElement('script')
					script.id = 'MathJax-script'
					// cdn引入比较慢
					script.src = 'https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js' 
					// script.src = 'static/tex-svg.js'; // 下载源码导入比较快，svg比chtml视觉上比较好
					// script.src = 'static/tex-chtml.js';
					document.head.appendChild(script)
				})();
				console.log("initMathJax()   window.MathJax", window.MathJax);
			},
			renderByMathjax: function(el) {
				// mathjax初始化后才会注入version
				if (!window.MathJax.version) {
					return
				}
				if (el && !Array.isArray(el)) {
					el = [el]
				}
				return window.MathJax.typesetPromise(el)
			}
		}

	}
</script>

<style>

</style>
