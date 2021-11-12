# Vue-5-模板语法-2


> 续上节，我们可以通过模板语法接收 `Vue` 的数据渲染，也可以通过 `Vue` 的指令实现不同类型的数据渲染和 `HTML` 属性的动态修改。

# 例：按钮的条件使能

假设，目前有一个需求是某个按钮需要根据某个字段的值进行使能和禁用。

### 代码

**`HTML` 代码**

```
 <div id="app5">
        <button v-bind:disabled="yy">{{ msg }}</button>
    </div>
```

**`JS` 代码**

```
var msg='点我'
        var app5 =new Vue({
            el: '#app5',
            data: {
                yy: 'true',
                msg: msg
                }
        })
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-22/1619074565265-image.png "页面效果")

**修改 `Vue` 实例的 `yy` 值为 `false`：**

![](https://gitee.com/phygerr/picture/raw/master/2021-4-22/1619074680222-image.png "页面效果")

# `Vue` 指令的缩写

v-作为 Vue 专属的视觉提示，用来标识 Vue 接管的元素，当你熟悉了 Vue 特性和项目全部在使用 Vue 前段框架的时候，我们可以使用 Vue 指令的缩写来简化代码。

### `v-bind` 缩写

缩写格式：`:`

```html
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a :[key]="url"> ... </a>
```

### `v-on` 缩写

缩写格式：`@`

```html
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a @[event]="doSomething"> ... </a>
```

> 在上面的动态参数缩写示例中，当 `event` 的值为 `"focus"` 时，`@:[event]` 将等价于 `v-on:focus`，即：当元素被聚焦时触发 `doSomething`。

# Tip

- `Vue` 也支持了 `js` 在模板语法中的执行。
- `Vue` 可以让我们对 `HTML` 元素的属性，比如 `ID，URl，Class` 等属性进行灵活的按需修改。

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。

