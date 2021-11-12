# Vue-4-模板语法-1


# 什么是模板语法

前面我们已经了解过 `HTML` 的模板语法，即插值表达式，双大括号的形式。

# 渲染

### 文本渲染-响应式

```html
<p>{{ judge }}</p>
```

以上代码中的模板，当 `judge` 的值发生变化时，模板中的值也会自动刷新，因为 `judge` 属性在 `Vue` 中是一个响应式对象。

### 文本渲染-单次

- 指令：v-once

```html
<p v-once>{{ judge }}</p>
```

以上代码中的，`v-once` 可以实现一次性的渲染，当数据改变时，插值处的内容不会更新。同时这个节点内的其他数据也不会更新。

### 单次渲染演示

**代码：**

```html
<div id="vif">
        <button v-on:click="func1">点我</button>
        <p v-once>{{ judge }}</p>
        <p v-if="judge">当点击上面的按钮时我会隐藏！</p>
        <button v-on:click="func2">点击跳转销毁Vue对象</button>

    </div>
```

**页面效果:**
![](https://gitee.com/phygerr/picture/raw/master/2021-4-22/1619072331221-image.png "页面效果")
点击`点我`，没有 `v-once` 标记时，`true` 会变为 `false`，而 `v-once` 标记后，`true` 则不会变化。

![](https://gitee.com/phygerr/picture/raw/master/2021-4-22/1619072487471-image.png "页面效果")
如上，数据已经隐藏，但是 `true` 未发生变化。

### HTML 渲染

- 指令：`v-html`

**代码：**

```html
<div id="app">
        <h1>{{ messages }}</h1>
        <button v-on:click='sj'>点我查看当前时间</button>
    </div>
```

`HTML` 格式的语言按照如上代码渲染时，默认不会处理 `HTML` 语言，效果如下：

![](https://gitee.com/phygerr/picture/raw/master/2021-4-22/1619072851467-image.png "页面效果")

**修改后的代码：**

```html
<div id="app">
        <h1><span v-html="messages"></span></h1>
        <button v-on:click='sj'>点我查看当前时间</button>
    </div>
```

加了 `v-html` 指令后的效果：

![](https://gitee.com/phygerr/picture/raw/master/2021-4-22/1619072962447-image.png "页面效果")

### HTML 属性渲染

- 指令：`v-bind:xx`

当我们需要在代码运行过程中修改元素属性时，我们可以采用 `v-bind` 对 `HTML` 元素属性进行修改。

**未绑定元素 ID 前的页面：**
![](https://gitee.com/phygerr/picture/raw/master/2021-4-22/1619073466890-image.png "页面效果")

**绑定属性代码（`HTML`）：**

```html
<div id="app">
        <h1 v-bind:id="demoId"><span v-html="messages"></span></h1>
        <button v-on:click='sj'>点我查看当前时间</button>
    </div>
```

**绑定属性代码（`JS`）：**

```js
var app1 = new Vue
        (
            {
                el: '#app',
                data:
                {
                    messages: 'hello Vue!',
                    demoId: 'HId'
                },
                methods:{
                    sj: function(){
                        this.messages='当前时间：' + new Date().toLocaleTimeString()
                    }
                }
            }
        )
```

**绑定元素 `ID` 后的页面：**

![](https://gitee.com/phygerr/picture/raw/master/2021-4-22/1619073590450-image.png "绑定ID")

**修改 `Vue` 属性 `demoId` 值后的页面：**

![](https://gitee.com/phygerr/picture/raw/master/2021-4-22/1619073659227-image.png "页面效果")

![](https://gitee.com/phygerr/picture/raw/master/2021-4-22/1619073686772-image.png "页面效果")

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。

