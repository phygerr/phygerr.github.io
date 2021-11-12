# Vue-11-条件渲染


# 条件渲染

当我们需要根据不同的条件对前端页面进行不同的渲染时，我们就需要用到条件渲染。`Vue` 为我们提供了 `v-if、v-else-if、v-else` 方法。

# 实践

## 代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
    <title>Document</title>
</head>
<body>
    <div id="app">
        请输入成绩等级：<input v-model="type">
        <br>
        <p>你输入的内容是：{{ type }}</p>

        <div v-if="type=='C'">
            <h1>及格</h1>
        </div>
        <div v-else-if="type=='A'">
            <h1>优秀</h1>
        </div>
        <div v-else>
            <h1>不及格</h1>
        </div>
    </div>

    <script>
        app = new Vue({
            el: "#app",
            data: {
                type: "C"
            }
        })
    </script>
</body>
</html>
```

## 页面效果

初始：

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620888915710-image.png)

输入 `A` 之后：

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620888900735-image.png)

输入其他值：

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620888947235-image.png)

# Tips

1. `v-model` 实现了输入框内容和数据的绑定。
2. `v-if` 等实现了根据数据的不同值展示不同的内容。
3. 在 `v-if` 模板中双引号内是单引号。

# 条件渲染的另一种方式

如上的形式是在页面中直接写上了 `v-if` 来进行条件判断，这样不是很优雅，我们尝试使用字典，根据不同的 `key` 来渲染不同的 `value` 来进行改造。

## 代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
    <title>Document</title>
</head>
<body>
    <div id="app">
        请输入成绩等级：<input v-model="type" placeholder="请输入正确的等级！(A,B,C,D)">
        <br>
        <p>你输入的内容是：{{ type }}</p>

       <h2>{{ res[type] }}</h2>
    </div>

    <script>
        app = new Vue({
            el: "#app",
            data: {
                type: "C",
                res: {"C":"及格","A":"优秀","B":"优良","D":"不及格"}
            }
        })
    </script>
</body>
</html>
```

## 页面效果

初始：

![初始](https://gitee.com/phygerr/picture/raw/master/2021-10-4/1633325090009-image.png "初始")

输入 `A`：

![输入A](https://gitee.com/phygerr/picture/raw/master/2021-10-4/1633325120423-image.png "输入A")

输入 `D`：

![输入D](https://gitee.com/phygerr/picture/raw/master/2021-10-4/1633325142738-image.png "输入D")

我们发现针对可以确定的条件和结果，使用字典的方式，页面代码更优雅。不过，`v-if` 使用起来也是非常不多呢！

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。
