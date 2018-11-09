# <scripts> 元素

`<script>`用于加载脚本。

它可以用于嵌入脚本代码。

```html
<script type="text/javascript">
  function hello() {
    console.log('hello world');
  }
</script>
```

该元素也可以用于嵌入外部脚本。

```html
<script type="text/javascript" src="example.js"></script>
```

一般情况下，浏览器遇到`<script>`元素就会等待脚本执行完，再继续往下渲染网页。因此该元素可能会堵塞网页渲染。

它有如下属性。

- async：可选，表示立刻下载外部脚本，但是不会堵塞页面渲染。一旦下载完毕，就立刻执行。该属性只对外部脚本有效。
- charset：可选，表示`src`属性指定的外部脚本的编码。
- defer：可选，表示该脚本可以推迟到页面渲染完成后执行。该属性只对外部脚本有效。
- src：可选，表示加载的外部脚本的地址。
- type：可选，表示脚本的类型，默认值是`text/javascript`。
