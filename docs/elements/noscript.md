# <noscript> 元素

`<noscript>`元素用于浏览器不支持 JavaScript 的情况（或关闭 JavaScript 支持），这时浏览器会显示这个元素指定的内容。如果浏览器支持 JavaScript，该元素就不会显示。

`<noscript>`元素里面可以包括任意 HTML 代码。

```html
<noscript>
  <p>当前页面要求 JavaScript 支持。</p>
</noscript>
```

由于搜索引擎会抓取`<noscript>`元素，所以对于那些 JavaScript 代码动态生成内容的网页，通常在`<noscript>`里面放置静态的、供搜索引擎使用的内容。
