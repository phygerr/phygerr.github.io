# Vue-13-Vif和Vshow的区别


# 背景

你可能已经知道 `Vue` 中有两个条件渲染方法，即 `v-if` 和 `v-show`，那么对于他两有什么却别和使用场景呢？今天我们就一起来看下。

# 实践

## v-if

### 特点

1. 真条件渲染（即要什么给什么）
2. 开销大
3. 适合低频操作
4. 节省内存
5. 可以处理 `else`

### 代码

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

### 页面效果

**初始：**

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620899134208-image.png)
**输入 A：**

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620899215895-image.png)

## v-show

### 特点

1. 假条件渲染（即一次全部给）
2. 开销小
3. 适合高频操作
4. 费内存
5. 无法处理 else

### 代码

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

        <div v-show="type=='C'">
            <h1>及格</h1>
        </div>
        <div v-show="type=='A'">
            <h1>优秀</h1>
        </div>
        <div v-show="type=='D'">
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

### 页面效果

**初始：**

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620898685635-image.png)
**输入 A：**

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620898747419-image.png)

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。
