# Vue-14-列表渲染v-for


# 前言

在前面的章节中，我们已经了解了关于 `Vue` 的条件渲染，今天我们就一起来看看 `Vue` 的列表渲染，即 `For` 循环。

# 例子

### v-for

和 `Python` 中的 `for` 循环一样，`Vue` 的列表渲染也遵循 `item in items` 的规范。`item` 为 `items` 中的元素别名。

### 代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
    <title>Vfor</title>
</head>
<body>
    <ol id="app">
        <li v-for="item in items" :key="item.title">
            {{ item.title }}
        </li>
    </ol>

    <script>
        app = new Vue({
            el: '#app',
            data:{
                "items":[
                    {title: 'phyger'},
                    {title: 'fly'}
                ]
                }
        })

    </script>
</body>
</html>
```

### 效果

![](https://gitee.com/phygerr/picture/raw/master/2021-6-17/1623919396534-image.png)

### v-for 中使用对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
    <title>Vfor</title>
</head>
<body>
    <div id="app">
    <ol>
        <li v-for="item in items" :key="item.title">
            {{ item.title }}
        </li>
    </ol>
    <h1>Authors Info</h1>
    <ul>
        <li v-for="value,key,index in objs">
            {{ index }} : {{ key }} : {{ value }}
        </li>
    </ul>
    </div>
    <script>
        app = new Vue({
            el: '#app',
            data:{
                "items":[
                    {title: 'phyger'},
                    {title: 'fly'}
                ],
                "objs": {
                    name: "phyger",
                    home: "xian",
                    age: 18
                }
                }
        })

    </script>
</body>
</html>
```

> 在对对象进行循环遍历的时候，`value`，`key`，`indx` 的顺序是固定的，即第一个参数获对象的值，最后一个参数获取索引。

### 效果

![](https://gitee.com/phygerr/picture/raw/master/2021-6-17/1623919892858-image.png)

### v-for 中使用 v-if

假如我们要遍历一个任务列表，但是只显示已完成的任务，此时我们就可以使用` v-for+v-if` 实现。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
    <title>Vfor</title>
</head>
<body>
    <div id="app">
    <ol>
        <li v-for="item in items" :key="item.title">
            {{ item.title }}
        </li>
    </ol>
    <h1>Authors Info</h1>
    <ul>
        <li v-for="value,key,index in objs">
            {{ index }} : {{ key }} : {{ value }}
        </li>
    </ul>

    <h1>v-if in v-for</h1>
    <ol>
        <li v-for="todo in todos" v-if="todo.status==1">
            {{ todo.name }}
        </li>
    </ol>
    </div>
    <script>
        app = new Vue({
            el: '#app',
            data:{
                "items":[
                    {title: 'phyger'},
                    {title: 'fly'}
                ],
                "objs": {
                    age: 18,
                    name: "phyger",
                    home: "xian"

                },
                todos: [
                    {name: 'eat',status: 1},
                    {name: 'work',status: 1},
                    {name: 'sleep',status: 0}
                ]
                }
        })

    </script>
</body>
</html>
```

> `v-if in v-for` 场景中`，v-for` 的优先级要高于 `v-if`，所以 `v-if` 会分别在每个 `for` 循环中重复运行。

### 效果

只显示 status=1 的任务。

![](https://gitee.com/phygerr/picture/raw/master/2021-6-17/1623921196743-image.png)

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。
