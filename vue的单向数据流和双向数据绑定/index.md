# Vue的单向数据流和双向数据绑定


# 前言

相信很多同学在学习 `Vue` 的时候，会经常用到或者被问题到单向数据流和双向数据绑定的概念，那它两到底有什么区别呢？我们一起来看看。

# 单向数据流

单向数据流在 `Vue` 中实际表现就是：当 `Model` 中的 `data` 发生变化的时候会单向修改 `View` 中的值，而 `View` 中的值发生变化的时候，`Model` 不会感知。实际应用就是 `v-bind` 单向数据。

# 双向数据绑定

和单向数据流相比，双向数据绑定就是多了 `View` 变化会通知到 `Model` 层。即 `MVVM` 的具体实现。无论 `Model` 还是 `View` 中的值发生变化，都会通过 `ViewModel` 通知到对方，实现同步。实际应用就是 `v-model` 双向数据绑定。

# 代码

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
		<title>单向&双向</title>
	</head>
	<body>
		<div id="app">
			<h1>单向数据流</h1>
			现在的时间是：{{ mytime }}
			<br>
			<button type="button" @click="shuax">刷新时间</button>
			<br><br>
			<hr >
			<h1>双向数据绑定</h1>
			<input v-model="sxbind"/>
			<br>
			你输入的数据是：{{ sxbind }}
		</div>

		<script type="text/javascript">
			app = new Vue({
				el: '#app',
				data: {
					mytime:new Date().toLocaleTimeString(),
					sxbind:''
				},
				methods: {
					shuax:function(){
						this.mytime = new Date().toLocaleTimeString();
					}
				}
			})
		</script>
	</body>
</html>
```

# 单向数据流效果

![↑ 初始页面](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5a89497ebc234bd5a94af6763b7f13aa~tplv-k3u1fbpfcp-zoom-1.image "初始页面")

![↑ 点击刷新时间（Model变化View也变）](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/af6d7f0ee9814da3af7629a5f983ea7a~tplv-k3u1fbpfcp-zoom-1.image "点击刷新时间")

![↑ Model变化View也变](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0dab00b5ddad43788bfa7f2cf773c42a~tplv-k3u1fbpfcp-zoom-1.image "Model变化View也变")

![↑ View变化Model不变](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/055aae02559a498ab2bfad63502d7ddc~tplv-k3u1fbpfcp-zoom-1.image "View变化Model不变")

# 双向数据绑定效果

![↑ Model变化View也变](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/69fd0976a0694c2d845276aed58e83cc~tplv-k3u1fbpfcp-zoom-1.image "Model变化View也变")

![↑ View变化Model也变](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/72cedb987c2d4a928f09257657ea3f0e~tplv-k3u1fbpfcp-zoom-1.image "Model变化View也变")

# 总结

单向数据流是通过 `props` 将 `Model` 层的变化通知到 `View` 层进行修改。双向数据绑定是通过 `Object.defineProperty()`的 `set()` 和 `get()` 方法来实现的，当某一方发生变化的时候，另一方就会收到更新值的提醒，从而实现数据同步变化。

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。

