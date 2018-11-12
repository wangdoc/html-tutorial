# <a> 元素

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
