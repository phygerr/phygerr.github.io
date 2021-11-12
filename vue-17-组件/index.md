# Vue-17-组件


# 什么是组件？

官方文档说，组件是带有名称的可复用实例。实际上你可以理解组件就是一个名为 `zj` 的 `html` 模板，当你要使用这个 `html` 模板的时候，你可以直接用 `zj` 标签即可。

# 组件初识

> 鉴于 `Vue3` 的逐步推广，所以从本篇文章开始，我们直接切换 `Vue3` 进行学习。

## 简单的例子

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>component</title>
        <script src="https://unpkg.com/vue@next"></script>
    </head>
    <body>
        <div id="app">
            <demo></demo>
        </div>

        <script type="text/javascript">
            // 创建一个Vue 应用
            const Vapp = Vue.createApp({})

            // 定义一个名为 demo的新全局组件
            // 在demo组件中嵌入全局组件demo1
            Vapp.component('demo', {
                template: '<div><h1>我的自定义组件!</h1><br><demo1></demo1></div>',
            })

            // 定义一个名为demo1的全局组件
            Vapp.component('demo1', {
                template: '<div><h2>我的demo1组件!</h2><br></div>',
            })

            // 将Vue的app挂载到app元素上
            Vapp.mount('#app')
        </script>
    </body>
</html>
```

![](https://gitee.com/phygerr/picture/raw/master/2021-7-16/1626425205450-image.png)

> 虽然我们只在 `body` 中使用 `demo` 组件，但是 `demo` 组件又内嵌了 `demo1` 组件，所以 `demo1` 的内容也会被展示。你大概可以感受到模块化的好处。

## 优点

由于组件可以复用的特点，当我们的组件被引用多次的时候，如果组件的内容发生变化，那我们直接修改源组件即可，引用它的地方都会自动刷新。

假设需要将 `demo1` 内容显示为红色，那么我们可以这样做：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>component</title>
        <script src="https://unpkg.com/vue@next"></script>
    </head>
    <body>
        <div id="app">
			第一次引用
            <demo></demo>
			<hr >
			第二次引用
			<demo></demo>
        </div>

        <script type="text/javascript">
            // 创建一个Vue 应用
            const Vapp = Vue.createApp({})

            // 定义一个名为 demo的新全局组件
            // 在demo组件中嵌入全局组件demo1
            Vapp.component('demo', {
                template: '<div><h1>我的自定义组件!</h1><br><demo1></demo1></div>',
            })

            // 定义一个名为demo1的全局组件
            Vapp.component('demo1', {
                template: '<div class="rd"><h2>我的demo1组件!</h2><br></div>',
            })

            // 将Vue的app挂载到app元素上
            Vapp.mount('#app')
        </script>

		<style type="text/css">
			.rd {
				color: #FF0000;
			}
		</style>
    </body>
</html>
```

![](https://gitee.com/phygerr/picture/raw/master/2021-7-16/1626426233563-image.png)

> 如上，组件 `demo1` 被引用了两次，当我们需要修改 `demo1` 的样式时，我们不需要你修改两次，只需要修改 `demo1` 组件的样式即可。

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。
