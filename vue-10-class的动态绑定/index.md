# Vue-10-Class的动态绑定


# 背景

当我们需要操作元素的 `class` 列表时，我们可以使用 `v-bind` 实现，但是直接计算整体字符显得很笨，针对这个问题，`Vue` 做了专门的加强，我们可以通过 `v-bind:class` 对 `class` 实现动态绑定。

# 实践

## 作用于对象(模板内联)

效果：我们可以通过操作 `Vue` 的 `attribute` 来实现对 `class` 的更改。

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
    <style type="text/css">
        .red {background-color: red}
        .bb {height: 400px;}
        .normal {width: 400px;}
        </style>
</head>
<body>
    <div id="vpp" class='normal' v-bind:class="{red:isred,bb:isbb}">
        <p>msg</p>
    </div>

    <script>
        app = new Vue({
            el: "#vpp",
            data: {
                isred: true,
                isbb: false
            }
        })
    </script>
</body>
</html>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620876317838-image.png)

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620876344672-image.png)

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620885336947-image.png)

### Tip

实际上，`class` 的动态绑定是通过 `Vue data` 属性的 `truthiness`（是否为真）来控制的。如果为真则加载 `class`，如果为假则不加载。

如上，当 `isbb` 为 `true` 时，`isbb` 对象的 `key==>bb` 样式才会加载。

> 默认样式为 `div` 宽 `400px`；背景颜色为红色。当我们修改 `isbb` 属性值后，`div` 的高度也变为 `400px`；

## 作用于对象(非模板内联)

上面的class是在模板语法内条件使能的，如果你觉得麻烦，也可以选择一下这种更直接的方法，即模板中定义对象的整体，Vue的data中定义对象的具体内容。

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
    <style type="text/css">
        .red {background-color: red}
        .bb {height: 400px;}
        .normal {width: 400px;}
        </style>
</head>
<body>
    <div id="vpp" class='normal' v-bind:class="clsObj">
        <p>msg</p>
    </div>
    <script>
        app = new Vue({
            el: "#vpp",
            data: {
                isred: true,
                isbb: false,
                clsObj: {
                    red: true,
                    bb: false
                }
            }
        })
    </script>
</body>
</html>
```

### 页面效果

和上面的一样

![](https://gitee.com/phygerr/picture/raw/master/2021-5-13/1620885832194-image.png)

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。
