# Vue-12-条件渲染（可重复元素）


# 背景

通常在我们的登录页面会有多种登录类型，我们可以通过条件渲染来切换不同的登录表单。

# 实践

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
        <template v-if="loginType=='username'">
        <label for="#user">username: </label> <input type="text" id="user">
        </template>
        <template v-else="loginType=='email'">
            <label for="#email">email: </label> <input type="email" id="email">
            </template>
        <br><br>
        <button @click='change'>点我切换登录方式</button>
    </div>

    <script>
        app = new Vue({
            el: "#app",
            data: {
                loginType: "username"
            },
            methods: {
                change: function(){
                    if(this.loginType=="username"){
                        this.loginType="email";
                    }else{
                        this.loginType="username";
                    }
                }
            }
        })
    </script>
</body>
</html>
```

### 页面效果

**初始：**

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620893218321-image.png)

**点击切换登录方式：**

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620893235227-image.png)

### 存在问题

当我们在 `username` 登录页面输入了信息后，再切换到 `email`，你会发现输入框中的内容还在，这是因为两种登录类型使用的输入框是同一个元素。`Vue` 为我们提供了解决方案，即给输入框加上 `key` 属性即可。

**切换前：**

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620893594875-image.png)

**切换后：**

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620893614134-image.png)

### 优化后的代码

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
        <template v-if="loginType=='username'">
        <label for="#user">username: </label> <input type="text" id="user" key="username-input">
        </template>
        <template v-else="loginType=='email'">
            <label for="#email">email: </label> <input type="email" id="email" key="email-input">
            </template>
        <br><br>
        <button @click='change'>点我切换登录方式</button>
    </div>

    <script>
        app = new Vue({
            el: "#app",
            data: {
                loginType: "username"
            },
            methods: {
                change: function(){
                    if(this.loginType=="username"){
                        this.loginType="email";
                    }else{
                        this.loginType="username";
                    }
                }
            }
        })
    </script>
</body>
</html>
```

### 页面效果

**切换前：**

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620893721993-image.png)

**切换后：**

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620893744755-image.png)

> 你会发现，加了 `key` 之后，在切换登录类型后，输入框中的内容已经被清理掉了。

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。

