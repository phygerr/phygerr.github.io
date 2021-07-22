# Vue-1-初识


# 什么是 Vue

众所周知，`Vue` 是前端领域知名的渐进式框架。有了它，我们不用直接操作 `DOM`，`Vue` 为我们提供了很多优雅的操作 `DOM` 的接口。使用 `Vue` 进行前端工程开发已经成为相当一部分开发者的选择。

# 如何使用 Vue

和其他框架一样，`Vue` 也拥有 `CDN` 在线加速资源，初学，我建议使用在线 `CDN` 进行学习。

## 推荐的 Vue 的 CDN 资源

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
```

你只需要将如上代码复制粘贴到 `HTML` 的 `head` 部分即可。

## Demo-1-模板渲染

此 `Demo` 实现通过 `Vue` 对 `DOM` 进行数据渲染。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{ messages }}</h1>
    </div>
    <script>
        var app1 = new Vue
        (
            {
                el: '#app',
                data:
                {
                    messages: 'hello Vue!'
                }
            }
        )
    </script>
</body>
</html>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-19/1618816648695-image.png "页面效果")

现在页面的模板对象已经被 `Vue` 渲染，数据和 `DOM` 进行了绑定，数据由 `Vue` 提供，那我们如何确认呢？

我们可以在控制台对 `Vue` 对象的数据元素进行修改，查看 `DOM` 会不会同步变化。

## 执行命令

```
app1.messages='hello Phyger!'
```

## 修改前

![](https://gitee.com/phygerr/picture/raw/master/2021-4-19/1618817088913-image.png "页面效果")

## 修改后

![](https://gitee.com/phygerr/picture/raw/master/2021-4-19/1618817137197-image.png "页面效果")

## Demo-2-实战

此实战利用数据渲染简单实现点击按钮，显示当前时间的功能。

### 代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{ messages }}</h1>
        <button v-on:click='sj'>点我查看当前时间</button>
    </div>
    <script>
        var app1 = new Vue
        (
            {
                el: '#app',
                data:
                {
                    messages: 'hello Vue!'
                },
                methods:{
                    sj: function(){
                        this.messages='当前时间：' + new Date().toLocaleTimeString()
                    }
                }
            }
        )
    </script>
</body>
</html>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-19/1618817700587-image.png "页面效果")

### 点击按钮后的效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-19/1618817721326-image.png "页面效果")

再点击一次

![](https://gitee.com/phygerr/picture/raw/master/2021-4-19/1618817740139-image.png "页面效果")

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。

