# Vue-8-计算属性和侦听属性



# 什么是侦听属性

上节，我们已经了解了计算属性和方法的区别，其实在 `Vue` 中还有一种可以根据 `Vue` 实例的数据而实时变化的属性，即侦听属性。由于这种属性的好处，你可能会滥用它，导致代码的臃肿。某些时候可能使用计算属性更合适。

# 实例

## 侦听属性

### 代码-HTML

```html
     <div id='app2'>
         {{ info }}
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
            }
        })
    </script>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-26/1619427171873-image.png "页面效果")

### 过程分析

如上，你会发现使用侦听属性在处理字符拼接的时候，定义了两个侦听属性，但是如果选择计算属性，则会简单甚多。

## 计算属性

### 代码-HTML

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
                infoc: function(){
                    return this.msg1+' '+this.msg2
                }
            }
        })
    </script>
```

### 页面效果

![](https://gitee.com/phygerr/picture/raw/master/2021-4-26/1619427598254-image.png "页面效果")

# 总结

侦听属性是针对单个属性的监听，即需要监听几个属性，就得写几个侦听方法；而计算属性可以以表达式的方式出现，即可以监控多个属性。侦听属性精确单一，计算属性一次到位。

关于侦听属性和计算属性的区别，你学废了吗？

> 以上就是今天的全部内容了，感谢您的阅读，我们下节再会。

{{% mermaid %}}
pie
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
{{% /mermaid %}}

{{% typeit code=java %}}
public class HelloWorld {
    public static void main(String []args) {
        System.out.println("Hello World");
    }
}
{{% /typeit %}}
