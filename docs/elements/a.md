# <a> 元素

## 简介

`<a>`标签用来定义一个链接（hyperlink），用户点击后，浏览器会跳转到指定的网址。

```html
<a href="https://wikipedia.org/">维基百科</a>
```

上面代码就定义了一个超级链接。浏览器显示“维基百科”，文字下面默认会有下划线，表示这是一个链接。用户点击后，浏览器跳转到`href`属性指定的网址。

## download 属性

`download`属性表示`<a>`元素点击后，浏览器会提示下载该文件。

```html
<a href="image.jpg" download>
```

上面代码中，浏览器不是跳转到`image.jpg`，而是提示下载到`image.jpg`。

`download`属性只有在设置了`href`属性时，才会生效。而且，该属性仅对同源的 URL 有效。

`download`属性的值默认是下载的文件名。由于该属性可写，所以可以指定下面的文件名。

```html
<a href="image.jpg" download="test.jpg">
```

上面代码点击后，浏览器会提示下载文件，文件名为`test.jpg`。

如果 HTTP 头信息`Content-Disposition`存在，并指定了文件名，那么这个文件名会覆盖`download`属性的文件名。
