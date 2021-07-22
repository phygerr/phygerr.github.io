# 掘金Markdown编辑器中的图片怎么居中？


# 背景

刚才在某群里无意间看到有位掘友提问：这个插入的图片怎么居中显示？其实我也早有这个疑问，只是懒得去处理。但是看到掘友有疑问，那作为热心肠的我必须帮他答疑解惑。

## 掘金原始居中方式

![1.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d63fadcb588f49a39beb6cd85bdcdadb~tplv-k3u1fbpfcp-watermark.image)

> 你会发现掘金原始的图片并不居中

# 尝试第1次

我们都知道，无论是Markdown还是富文本编辑器，最终在网页上的呈现方式都是一样的，无非是HTML+CSS+JS，通过以上简单的理论，我们开始第一次尝试，计划直接将Markdown的图片展示方式用HTML的`<img>`标签替代。

## 代码

```html
<img style="align:center" src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58935071dcee4613bf27ec6e9bb10bc6~tplv-k3u1fbpfcp-watermark.image" />
```

## 效果

<img style="align:center" src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58935071dcee4613bf27ec6e9bb10bc6~tplv-k3u1fbpfcp-watermark.image" />

> 你会发现依然不居中，原因竟是直接在`img`标签中添加的样式竟然没有生效，证据如下。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2a1f113d7d3143b6a143674f2ed137c6~tplv-k3u1fbpfcp-watermark.image)

# 尝试第2次

经过上面的失败，我们决定换一种方式，即直接使用`style`标签来定义样式。

## 代码

```html
<style type="text/css">
img {align:center}
</style>
<img style="align:center" src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58935071dcee4613bf27ec6e9bb10bc6~tplv-k3u1fbpfcp-watermark.image" />
```

## 效果
<style type="text/css">
img {align:center}
</style>
<img style="align:center" src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58935071dcee4613bf27ec6e9bb10bc6~tplv-k3u1fbpfcp-watermark.image" />

-_-//    简直没脸看啊，样式直接漏了。

# 尝试第3次

经过上面的失败，我决定了这次再不成功，我就弃笔从戎了！估计我这小身板儿也进不了部队，哈哈哈。这次我们计划用`div`包裹`img`标签，因为通常前端都是这么干的。

## 代码

```html
<div align=center>
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58935071dcee4613bf27ec6e9bb10bc6~tplv-k3u1fbpfcp-watermark.image" />
</div>
```

## 效果
<div align=center>
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58935071dcee4613bf27ec6e9bb10bc6~tplv-k3u1fbpfcp-watermark.image" />
</div>

(#^.^#)，我去，终于成了。虽然这是很简单的基操，但是能够帮到掘友，我还是很开心的。

# 多说一句

通过这篇文章，我建议各位掘友能够动手去设计属于自己的主题并且贡献给社区，这样对于推动社区体验无疑是一件小但很好的事情。

> 以上就是本文的全部内容，如果喜欢记得（四连）：点赞，评论，收藏，转发。

