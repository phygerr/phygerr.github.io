# Vue-3-生命周期管理


# 生命周期钩子

和传统的对象一样，`Vue` 的实例对象也有完整的生命周期过程，在这个过程中 Vue 为我们提供了不用阶段的钩子，机生命周期函数。如果你在实例中声明了这些方法，它们会在对应的阶段自动触发。

# 生命周期流程图

![](https://gitee.com/phygerr/picture/raw/master/2021-4-21/1618994351875-image.png "生命周期流程图")
_上图摘自：`cn.vuejs.org`_

# 演示

我们通过以下代码来对 `Vue` 实例对象的生命周期进行详细的展示。

### 生命周期阶段

1. beforeCreate
2. created
3. beforeMount
4. mounted
5. beforeUpdate
6. updated
7. beforeDestroy
8. destroyed

### 代码

```
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
        <p>{{ judge }}</p>
        <p v-if="judge">当点击上面的按钮时我会隐藏！</p>
        <button v-on:click="func2">点击跳转销毁Vue对象</button>

    </div>

    <script>

        var judge=true

        var app4 = new Vue({
            el:'#vif',
            data:{
                judge:judge
            },
            methods:{
                func1:function(){
                    if(this.judge == true){
                        this.judge=false;
                    }else{
                        this.judge=true;}

                },
                func2:function(){
                    this.$destroy();
                }
            },
            beforeCreate:function(){
                console.log('Vue instance ready2Create...')
            },
            created:function(){
                console.log('Vue instance created...')
            },
            beforeUpdate:function(){
                console.log('Vue instance beforeUpdate...')
            },
            updated:function(){
                console.log('Vue instance updated...')
            },
            beforeMount:function(){
                console.log('Vue instance beforeMounte...')
            },
            mounted:function(){
                console.log('Vue instance mounted...')
            },
            beforeDestroy:function(){
                console.log('Vue instance beforeDestroy...')
            },
            destroyed:function(){
                console.log('Vue instance destroyed...')
            }
        })
    </script>
</body>
</html>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-21/1618995819567-image.png "页面效果")

如上，当我们打开页面的时候，`Vue` 已经完成了 `4` 个阶段。

### 触发 update

点击`点我`，查看控制台日志

![](https://gitee.com/phygerr/picture/raw/master/2021-4-21/1618996020936-image.png "控制台日志")

### 触发 destroy

点击`点击跳转销毁Vue对象`，查看控制台日志

![](https://gitee.com/phygerr/picture/raw/master/2021-4-21/1618996085354-image.png "控制台日志")

怎么样，`Vue` 实例的声明周期你学废了吗？

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。

