# Vue-2-常用指令


# 指令

`Vue` 中，有很多常用的指令，你可以理解它是可以绑定在指定的 `action` 上的。

# 实例

## v-bind

`v-bind` 就是 `Vue` 中一个常见的指令，其中 `v-` 前缀代表这是 `Vue` 为我们提供的指令，下面的例子将实现鼠标悬停在被绑定的元素上后显示它的 `title` 信息。

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
    <div id="vb">
        <span v-bind:title="info">悬停显示</span>
    </div>

    <script>
        var app2 = new Vue
        ({
                el: '#vb',
                data: {
                    info: '此页面加载于：' + new Date().toLocaleString()
                }
            })
    </script>
</body>
</html>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-21/1618972525475-image.png "页面效果")

## v-if

此指令可以实现条件判断，以下实例可以实现当点击按钮时，通过判断绑定元素的 `judge` 属性，进行元素的显示和隐藏。

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

    <div id="vif">
        <button v-on:click="func1">点我</button>
        <p v-if="judge">当点击上面的按钮时我会隐藏！</p>
    </div>


    <script>
        var app4 = new Vue({
            el:'#vif',
            data:{
                judge:true
            },
            methods:{
                func1:function(){
                    if(this.judge == true){
                        this.judge=false;
                    }else{
                        this.judge=true;}

                }
            }
        })
    </script>
</body>
</html>
```

> 以上代码中，`v-on` 是用来监听元素的事件，当事件发生的时候会触发对应的方法。

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-21/1618972860919-image.png "页面效果")

点击按钮

![](https://gitee.com/phygerr/picture/raw/master/2021-4-21/1618972880777-image.png "页面效果")

再次点击

![](https://gitee.com/phygerr/picture/raw/master/2021-4-21/1618972901524-image.png "页面效果")

## v-for

`v-for` 可以实现对元素的 `for` 循环，以下实例可以实现页面元素的循环渲染，`Vue` 提供可遍历数据。

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

    <div id="floop">
        <ol>
            <li v-for="i in is">
                {{ i }}
            </li>
        </ol>
    </div>

    <script>
        var app3 = new Vue({
            el: '#floop',
            data:{
                is:[
                    '西安',
                    '北京',
                    '上海'
                ]
            }
        })
    </script>
</body>
</html>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-21/1618973143742-image.png "页面效果")

### v-for 进阶

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

    <div id="floop">
        <ul>
            <li v-for="i in is">
                {{ i.name }}: {{ i.goods }}
            </li>
        </ul>
    </div>

    <script>
        var app3 = new Vue({
            el: '#floop',
            data:{
                is:[
                    {'name': '西安','goods': '面食'},
                    {'name': '北京','goods': '肉食'},
                    {'name': '上海','goods': '菜食'}
                ]
            }
        })
    </script>

</body>
</html>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-21/1618973426332-image.png "页面效果")

**Tip:** 如上，`Vue` 的 `Observer` 帮我们将普通的 `DOM` 对象转换成了响应式对象。

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。

