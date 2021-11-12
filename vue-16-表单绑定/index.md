# Vue-16-表单绑定


> 方便演示，代码中只贴了 `body` 内容。

# 前言

我们知道 `v-model` 是双向数据绑定的代表。今天我们就一起来深入了解 `v-model` 表单绑定的更多内容。

# 使用场景

我们可以使使用` v-model` 监听 `input`，`textarea`，`select` 元素上创建双向数据绑定，也可以根据 `checkbox` 和 `radio` 的 `checked` 和 `change` 事件来实现数据绑定，具体如下：

```
1、text 和 textarea 元素使用 value property 和 input 事件；
2、checkbox 和 radio 使用 checked property 和 change 事件；
3、select 字段将 value 作为 prop 并将 change 作为事件。
```

# 实例

## 文本绑定

```html
<body>
    <div id="appv">
        请输入内容:
        <input v-model="info">
        <p>你输入的内容是：{{ info }}</p>
    </div>
    <script>
        app = new Vue({
            el: "#appv",
            data: {
                info: "placeholder",
            }
        })
    </script>
</body>
```

![文本绑定效果](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625642903182-image.png)

## 多行文本绑定

```html
<body>
    <div id="appv">
        请输入内容:<br><br>
		<textarea rows="" cols="" v-model="info"></textarea>
        <p style="white-space: pre-line;">你输入的内容是：<br><br>{{ info }}</p>
    </div>
    <script>
        app = new Vue({
            el: "#appv",
            data: {
                info: "placeholder",
            }
        })
    </script>
</body>
```

![多行文本绑定效果](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625643349384-image.png)

## 复选框

`v-model` 可以智能的将 `v-model` 的值绑定到 `checked` 属性中，从而实现选定与取消选定。

### 单个复选框，绑定到布尔值

```html
	<body>
		<div id="app">
			<label for="ck">{{ ckb }}</label>
			<input id="ck" type="checkbox" v-model="ckb">

		</div>

		<script type="text/javascript">
			app = new Vue({
				el: "#app",
				data: {
					ckb: true
				}
			})
		</script>
	</body>
```

![选定的效果](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625647670261-image.png)

![取消选定的效果](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625647695413-image.png)

### 多个复选框，绑定到同一数组

```html
<body>
		<div id="app">
			<label for="ck">{{ ckb }}</label>
			<input id="ck" type="checkbox" v-model="ckb">

			<div class="mui-input-row mui-checkbox ">
				<label for="c1">P1</label>
				<input id="c1" type="checkbox" v-model="persons" value="中国人">

				<label for="c2">P2</label>
				<input id="c2" type="checkbox" v-model="persons" value="德国人">

				<label for="c3">P3</label>
				<input id="c3" type="checkbox" v-model="persons" value="俄罗斯人">

				<p>您的选择的是:{{ persons }}</p>
			</div>

		</div>

		<script type="text/javascript">
			app = new Vue({
				el: "#app",
				data: {
					ckb: true,
					persons: []
				}
			})
		</script>
	</body>
```

> 多个复选框使用用一个 `v-model`，此时复选框被选中时，复选框的 `value` 会被自动添加到 `v-model` 绑定的数组中去。

![选则一个的效果](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625649942132-image.png)

![选择多个的效果](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625649962973-image.png)

## 单选框

当单选框的选择发生变化的时候，`v-model` 绑定的值会自动切换为当前选择的单选框的 `value` 值。

```html
<body>
		<div id="app">
			<div class="mui-input-row mui-radio ">
				<label for="r1">中国</label>
				<input id="r1" type="radio" v-model="info" value="伟大的国家！" checked>
				<br>
				<label for="r2">日本</label>
				<input id="r2" type="radio" v-model="info" value="二战战败国！">
				<br>
				<p>对应国家的描述：{{ info }}</p>
			</div>
		</div>

		<script type="text/javascript">
			app =new Vue({
				el: "#app",
				data: {
					info: ""
				}
			})
		</script>
	</body>
```

![选择中国](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625650409671-image.png)

![选择日本](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625650438207-image.png)

## 下拉选框

`v-model` 绑定的值会根据下拉选框选择的值自动发生变化。

### 单选时 v-model 绑定的是字符串

```html
<body>
		<div id="app">
			<select name="ABC" v-model="select">
				<option disabled="" value="">请选择</option>
				<option value ="A-value">A</option>
				<option value ="B-value">B</option>
				<option value ="C-value">C</option>
			</select>

			<p>您选择的选项的value是：{{ select }}</p>
		</div>

		<script type="text/javascript">
			app = new Vue({
				el: "#app",
				data: {
					select: ""
				}
			})
		</script>
	</body>
```

![初始效果](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625650897623-image.png)

![选择A的效果](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625650906584-image.png)

### 多选时 v-model 绑定的是数组

即使 `v-model` 绑定的元数据类型是字符，也会被 `Vue` 强制转换为数组。

```html
<body>
		<div id="app">
			<select name="ABC" v-model="select" multiple="multiple">
				<option value ="A-value">A</option>
				<option value ="B-value">B</option>
				<option value ="C-value">C</option>
			</select>

			<p>您选择的选项的value是：{{ select }}</p>
		</div>

		<script type="text/javascript">
			app = new Vue({
				el: "#app",
				data: {
					select: ""
				}
			})
		</script>
	</body>
```

![初始效果](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625651066588-image.png)

![选择B的效果](https://gitee.com/phygerr/picture/raw/master/2021-7-7/1625651081125-image.png)

### 动态渲染（循环）@下拉框的值绑定

对于列表选项很多，且需要动态调整的拉下选框，我们可以使用 `v-for` 加 `v-bind` 对选项的内容进行循环展示。

```html
<body>
		<div id="app">
			<select v-model="kvs">
				<option v-for=" item in items" v-bind:value="item.v">{{ item.k }}</option>
			</select>
			<p>您选择的选项的value是：{{ kvs }}</p>
		</div>

		<script type="text/javascript">
			app = new Vue({
				el: "#app",
				data: {
					kvs: '<待选择>',
					items: [
						{k:"中国",v:"伟大的国家"},
						{k:"美国",v:"强大的国家"},
						{k:"日本",v:"猥琐的国家"}
					]
				}
			})
		</script>
	</body>
```

![初始效果](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625710155228-image.png)

![选择中国的效果](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625710169549-image.png)

## 值绑定

通常，对于选中的复选框，`v-model` 绑定的值是布尔。单选框和下拉选框选中时，`v-model` 取的是 `value` 的值。

如果我们想要自定义选中时的值，我们就需要使用 `v-bind` 等方式来绑定值。

### 复选框的值绑定

```html
<body>
		<div id="app">
			<div class="mui-input-row mui-checkbox mui-left">
			  <label for="checkbox1" >{{ c1 }}</label>
			  <input id="checkbox1" type="checkbox" v-model="c1" true-value='选中了' false-value='没选中' checked>

			</div>

		</div>

		<script type="text/javascript">
			app = new Vue({
				el: "#app",
				data: {
					c1: "选中了"
				}
			})
		</script>
	</body>
```

![初始效果](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625710990950-image.png)

![取消选择效果](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625710998812-image.png)

### 单选框的值绑定

```html
<body>
		<div id="app">
			<div class="mui-input-row mui-checkbox mui-left">
			  <label for="checkbox1" >{{ c1 }}</label>
			  <input id="checkbox1" type="checkbox" v-model="c1" true-value='选中了' false-value='没选中' checked>

			</div>

			<br>
				<div class="mui-input-row mui-radio ">
					<label for="r1">A</label>
					<input id="r1" type="radio" checked v-model="RR" v-bind:value="vv.a">

					<label for="r2">B</label>
					<input id="r2" type="radio" v-model="RR" v-bind:value="vv.b">

					<label for="r3">C</label>
					<input id="r3" type="radio" v-model="RR" v-bind:value="vv.c">
					<br>
					你选了：{{ RR }} ！
				</div>

		</div>

		<script type="text/javascript">
			app = new Vue({
				el: "#app",
				data: {
					c1: "选中了",
					RR: "选中了A",   // RR为选中了A时，Vue会自动将radio checked，RR值为null时，Vue会自动将radio unchecked
					vv: {
						a: "选中了A",
						b: "选中了B",
						c: "选中了C"
					}
				}
			})
		</script>
	</body>
```

![初始效果](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625712168463-image.png)

![选择C后的效果](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625712179109-image.png)

## 修饰符

### .lazy

在默认情况下，`v-model` 在每次 `input` 事件触发后将输入框的值与数据进行同步，如果你想要在 `change` 事件后再同步，那么你可能需要使用 `lazy` 修饰符。

```html
<body>
		<div id="app">
			<input type="text" v-model="msg" placeholder="请输入"/>
			<br>
			<span>
				你最终输入的是：{{ msg }}
			</span>
		</div>

		<script type="text/javascript">
			app = new Vue({
				el: "#app",
				data: {
					msg: ""
				}
			})
		</script>
	</body>
```

![初始效果](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625725065095-image.png)

![输入过程中](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625725093850-image.png)

![输入结束触发change](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625725110765-image.png)

### .number

如果想自动将用户的输入值转为数值类型，可以给 `v-model` 添加 `number` 修饰符。

```
<input v-model.number="age" type="number">
```

这通常很有用，因为即使在 `type="number"` 时，`HTML` 输入元素的值也总会返回字符串。如果这个值无法被 `parseFloat()` 解析，则会返回原始的值。

### .trim

如果要自动过滤用户输入的首尾空白字符，可以给 `v-model` 添加 `trim` 修饰符。

```html
<body>
		<div id="app">
			<input type="text" v-model.lazy.trim="msg" placeholder="请输入"/>
			<br>
			<span>
				你最终输入的是：前{{ msg }}后
			</span>
		</div>

		<script type="text/javascript">
			app = new Vue({
				el: "#app",
				data: {
					msg: ""
				}
			})
		</script>
	</body>
```

![初始效果](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625725430585-image.png)

![输入过程中](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625725506706-image.png)

![输入结束触发change](https://gitee.com/phygerr/picture/raw/master/2021-7-8/1625725558320-image.png)

> 你会发现文本前后的空格都被过滤掉了，但是文本中间的空格不会被过滤。

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。
