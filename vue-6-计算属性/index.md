# Vue-6-计算属性


# 什么是计算属性

理论上在模板的插值表达式中，我们可以进行简单运算，但是在模板表达式中加入太多的逻辑，会让模板太复杂不方便维护。

# 实践

## demo1

当我们想要根据出生年份来计算年龄的时候，我们可以这样做：

### 代码-HTML

```html
    <div id="app1">
       phyger的年龄是多少？
       <br>
       {{ 2021-Number(birth) }}
    </div>
```

### 代码-JS

```js
<script>
        var integer
        var app = new Vue({
            el: "#app1",
            data: {
                birth: 1992
            }
        })
    </script>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-26/1619405343559-image.png "页面效果")
如上，`2001` 年出生的孩子，今年应该是 `20` 岁。

---

以上方式，我们在模板插值表达式中进行了计算，现在我们使用 `Vue` 的计算属性来对它进行替代。

### 代码-HTML

```html
    <div id="app1">
       phyger的年龄是多少？
       <br>
       {{ age }}
    </div>
```

### 代码-JS

```js
    <script>
        var integer
        var app = new Vue({
            el: "#app1",
            data: {
                birth: 1992
            },
            computed: {
                age: function(){
                    return 2021-this.birth
                }
            }
        })
    </script>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-26/1619405719534-image.png "页面效果")

## demo2

根据出生日期计算年龄。

### 代码-HTML

```html
 <div id="app1">
	 根据出生年份计算年龄！
	 <input type="datetime" v-model="birth"/>
	 <br>
	 {{ age }}
  </div>
```

### 代码-JS

```js
<script>
        var app = new Vue({
            el: "#app1",
            data: {
                birth: 1992
            },
            computed: {
                age: function(){
                    console.log('computed start...')
                    return 2021-this.birth
                }
            },
        })
    </script>
```

### 效果

![输入出生年份自动计算出年龄](https://gitee.com/phygerr/picture/raw/master/2021-9-29/1632894666991-image.png "输入出生年份自动计算出年龄")

# 问题

如果我们使用一个非响应式的对象，比如 `Data`，那么当 `Vue` 的属性发生变化时，这个非响应式的对象会变吗？

### 代码-HTML

```html
 <div id="app1">
	 根据出生年份计算年龄！
	 <input type="datetime" v-model="birth"/>
	 <br>
	 {{ age }}
  </div>
```

### 代码-JS

```js
<script>
		const nowDate = new Date();
        var app = new Vue({
            el: "#app1",
            data: {
                birth: 1992
            },
            computed: {
                age: function(){
                    console.log('computed start...')
                    //return 2021-this.birth
					return nowDate.getSeconds()
                }
            },
        })
    </script>
```

### 效果

你会发现，当输入框的值发生变化的时候，`Vue` 的 `age` 属性未发生变化。

![age为10](https://gitee.com/phygerr/picture/raw/master/2021-9-29/1632896210907-image.png "页面效果")

![age依然为10](https://gitee.com/phygerr/picture/raw/master/2021-9-29/1632896235517-image.png "页面效果")

> 具体原因我们下节继续分析。
>
> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。

