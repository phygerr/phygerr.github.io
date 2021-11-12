# Vue-15-事件绑定


# 前言

前面我们已经了解了条件渲染和列表渲染，计算属性动态绑定等。今天我们学习一个常用的概念：事件绑定，即在事件被触发时执行某些动作。

# 事件监听

### 代码

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
		<title>von</title>
	</head>
	<body>
		<div id="app">
			<h1>v-on中直接执行代码进行计算</h1>
			<button v-on:click="counter += 1">点一下</button>
			<p>你点击了 {{counter}} 下！</p>

			<h1>v-on中调用方法showinfo</h1>
			<button type="button" @click="showinfo">点击查看提示</button>
		</div>
		<script type="text/javascript">
		//
		//                  江城子 . 程序员之歌
		//
		//              十年生死两茫茫，写程序，到天亮。
		//                  千行代码，Bug何处藏。
		//              纵使上线又怎样，朝令改，夕断肠。
		//
		//              领导每天新想法，天天改，日日忙。
		//                  相顾无言，惟有泪千行。
		//              每晚灯火阑珊处，夜难寐，加班狂。
		//
			app = new Vue({
				el: '#app',
				data: {
					counter: 0,
					name: "phyger"
				},
				methods:{
					showinfo: function(event){
						alert('Hello '+this.name+' !');
						console.log(event);
					}
				}
			})
		</script>
	</body>
</html>
```

### 效果

1. `v-on` 监听 `click` 事件，当发生鼠标点击事件时 `Vue` 会进行 `counter` 加 1 的动作。
2. `v-on` 监听 `click` 事件，当发生鼠标点击事件时调用 `showinfo` 方法。

![浏览器效果](https://gitee.com/phygerr/picture/raw/master/2021-6-18/1623995612652-image.png)

# 事件参数传递&修饰

### 代码:参数传递

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
		<title>von</title>
	</head>
	<body>
		<div id="app">
			<h1>v-on中直接执行代码进行计算</h1>
			<button v-on:click="counter += 1">点一下</button>
			<p>你点击了 {{counter}} 下！</p>

			<h1>v-on中调用方法showinfo</h1>
			<button type="button" @click="showinfo">点击查看提示</button>

			<h1>say something</h1>
			<button type="button" @click="say('good')">say good</button>
			<button type="button" @click="say('bad')">say bad</button>
		</div>
		<script type="text/javascript">
		//
		//                  江城子 . 程序员之歌
		//
		//              十年生死两茫茫，写程序，到天亮。
		//                  千行代码，Bug何处藏。
		//              纵使上线又怎样，朝令改，夕断肠。
		//
		//              领导每天新想法，天天改，日日忙。
		//                  相顾无言，惟有泪千行。
		//              每晚灯火阑珊处，夜难寐，加班狂。
		//
			app = new Vue({
				el: '#app',
				data: {
					counter: 0,
					name: "phyger"
				},
				methods:{
					showinfo: function(event){
						alert('Hello '+this.name+' !');
						console.log(event);
					},
					say: function(sm,event){
						console.log('say '+ sm);
					}
				}
			})
		</script>
	</body>
</html>
```

### 效果

分别点击 `say good` 和 `say bad` 将会传递不同的参数到方法 `say` 中，从而实现不同的效果。

![](https://gitee.com/phygerr/picture/raw/master/2021-6-18/1623996261334-image.png)

### 代码：修饰符

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
		<title>von</title>
	</head>
	<body>
		<div id="app">
			<h1>v-on中直接执行代码进行计算</h1>
			<button v-on:click="counter += 1">点一下</button>
			<p>你点击了 {{counter}} 下！</p>

			<h1>v-on中调用方法showinfo</h1>
			<button type="button" @click="showinfo">点击查看提示</button>

			<h1>say something</h1>
			<button type="button" @click.once="say('good')">say good</button>
			<button type="button" @click="say('bad')">say bad</button>
		</div>
		<script type="text/javascript">
		//
		//                  江城子 . 程序员之歌
		//
		//              十年生死两茫茫，写程序，到天亮。
		//                  千行代码，Bug何处藏。
		//              纵使上线又怎样，朝令改，夕断肠。
		//
		//              领导每天新想法，天天改，日日忙。
		//                  相顾无言，惟有泪千行。
		//              每晚灯火阑珊处，夜难寐，加班狂。
		//
			app = new Vue({
				el: '#app',
				data: {
					counter: 0,
					name: "phyger"
				},
				methods:{
					showinfo: function(event){
						alert('Hello '+this.name+' !');
						console.log(event);
					},
					say: function(sm,event){
						console.log('say '+ sm);
					}
				}
			})
		</script>
	</body>
</html>
```

> 如上，我们为 `say good` 的按钮的 `click` 事件添加了 `once` 的修饰符，意为这个事件仅会触发一次 `say` 方法。

### 效果

![浏览器截图](https://gitee.com/phygerr/picture/raw/master/2021-6-18/1623996642284-image.png)

当我们第二次点击 `say good` 按钮时，`say` 方法已经不会被触发了，而 `say bad` 按钮则可以多次触发 `say` 方法。

### 常用的事件修饰符

1. stop
2. prevent
3. capture
4. self
5. once
6. passive

### 常用的按键修饰符

鼠标：

1. left
2. right
3. middle

键盘：

1. ctrl
2. alt
3. shift
4. meta

### 按键修饰符

`v-on` 监听键盘事件，当发生对应事件触发某些操作。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
		<title>von</title>
	</head>
	<body>
		<div id="app">
			<h1>v-on中直接执行代码进行计算</h1>
			<button v-on:click="counter += 1">点一下</button>
			<p>你点击了 {{counter}} 下！</p>

			<h1>v-on中调用方法showinfo</h1>
			<button type="button" @click="showinfo">点击查看提示</button>

			<h1>say something</h1>
			<button type="button" @click.once="say('good')">say good</button>
			<button type="button" @click="say('bad')">say bad</button>

			<h1>push mouse middle</h1>
			<button type="button" @click.middle="f1">mouse middle active alert</button>
		</div>
		<script type="text/javascript">
		//
		//                  江城子 . 程序员之歌
		//
		//              十年生死两茫茫，写程序，到天亮。
		//                  千行代码，Bug何处藏。
		//              纵使上线又怎样，朝令改，夕断肠。
		//
		//              领导每天新想法，天天改，日日忙。
		//                  相顾无言，惟有泪千行。
		//              每晚灯火阑珊处，夜难寐，加班狂。
		//
			app = new Vue({
				el: '#app',
				data: {
					counter: 0,
					name: "phyger"
				},
				methods:{
					showinfo: function(event){
						alert('Hello '+this.name+' !');
						console.log(event);
					},
					say: function(sm,event){
						console.log('say '+ sm);
					},
					f1: function(){
						alert("U clicked mouse middle!")
					}
				}
			})
		</script>
	</body>
</html>

```

### 效果

![鼠标右键触发alert](https://gitee.com/phygerr/picture/raw/master/2021-6-18/1623998016011-image.png)

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。
