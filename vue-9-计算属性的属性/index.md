# Vue-9-计算属性的属性


# 计算属性的属性

默认的，计算属性实现了 `getter` 属性，我们可以直接拿到计算属性的值。但是如果尝试对计算属性的值进行修改，会成功吗？

![](https://gitee.com/phygerr/picture/raw/master/2021-4-26/1619428201293-image.png)

如上，不出意外的在对计算属性进行 `setter` 操作的时候失败了，`Vue` 提示我们计算属性 `infoc` 没有 `setter` 属性。

# 实现计算属性的 setter 属性

### 代码-HTMl

```html
     <div id='app2'>
         {{ infoc }}
     </div>
```

### 代码-JS

```js
    <script>
        var app2 = new Vue({
            el: "#app2",
            data: {
                msg1: "hello",
                msg2: "phyger",
                info: "hello phyger"
            },
            watch:{
                msg1: function(){
                    this.info = this.msg1 + ' ' + this.msg2
                },
                msg2: function(){
                    this.info = this.msg1 + ' ' + this.msg2
                }
            },
            computed: {
                infoc:{
                    get: function(){
                        return this.msg1+' '+this.msg2
                    },
                    set: function(newValue){
                        var temInfo = newValue.split(' ')
                        this.msg1=temInfo[0]
                        this.msg2=temInfo[temInfo.length-1]
                    }
                }
            }
        })
    </script>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-26/1619428823851-image.png)

可以看到，在计算属性中实现 `setter` 属性后，计算属性已经可以进行赋值操作了。而且在赋值过程中，`msg1` 和 `msg2` 的值都发生了变化。

# Tip

在计算属性中定义 `setter` 属性的时候，`infoc` 已经由原来的方法变成了方法的集合。且默认的 `getter` 属性也要重新定义。

## 不定义会如何？

如果不重新定义，则 Vue 对象会由于 Getter 属性的缺失而无法渲染：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script crossorigin="anonymous" integrity="sha512-qRXBGtdrMm3Vdv+YXYud0bixlSfZuGz+FmD+vfXuezWYfw4m5Ov0O4liA6UAlKw2rh9MOYULxbhSFrQCsF1hgg==" src="https://lib.baomitu.com/vue/2.6.14/vue.common.dev.js"></script>
</head>
<body>
    <div id="app2">
        {{ infoc }}
    </div>
    <script>
        var app2 = new Vue({
            el: "#app2",
            data: {
                msg1: "hello",
                msg2: "phyger",
                info: "hello phyger"
            },
            watch:{
                msg1: function(){
                    this.info = this.msg1 + ' ' + this.msg2
                },
                msg2: function(){
                    this.info = this.msg1 + ' ' + this.msg2
                }
            },
            computed: {
                infoc:{
                    // get: function(){
                    //     return this.msg1+' '+this.msg2
                    // },
                    set: function(newValue){
                        var temInfo = newValue.split(' ')
                        this.msg1=temInfo[0]
                        this.msg2=temInfo[temInfo.length-1]
                    }
                }
            }
        })
    </script>
</body>
</html>
```

![提示Getter属性缺失](https://gitee.com/phygerr/picture/raw/master/2021-10-2/1633179450200-image.png "Getter属性缺失")

**将 get 属性的注释去掉**

![页面已经渲染正常](https://gitee.com/phygerr/picture/raw/master/2021-10-2/1633179590066-image.png "页面已经渲染正常")

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。
