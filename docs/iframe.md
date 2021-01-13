# iframe

`<iframe>`标签用于在网页里面嵌入其他网页。

## 基本用法

`<iframe>`标签生成一个指定区域，在该区域中嵌入其他网页。它是一个容器元素，如果浏览器不支持`<iframe>`，就会显示内部的子元素。

```html
<iframe src="https://www.example.com"
        width="100%" height="500" frameborder="0"
        allowfullscreen sandbox>
  <p><a href="https://www.example.com">点击打开嵌入页面</a></p>
</iframe>
```

上面的代码在当前网页嵌入`https://www.example.com`，显示区域的宽度是`100%`，高度是`500`像素。如果当前浏览器不支持`<iframe>`，则会显示一个链接，让用户点击。

浏览器普遍支持`<iframe>`，所以内部的子元素可以不写。

`<iframe>`的属性如下。

- `allowfullscreen`：允许嵌入的网页全屏显示，需要全屏 API 的支持，请参考相关的 JavaScript 教程。
- `frameborder`：是否绘制边框，`0`为不绘制，`1`为绘制（默认值）。建议尽量少用这个属性，而是在 CSS 里面设置样式。
- `src`：嵌入的网页的 URL。
- `width`：显示区域的宽度。
- `height`：显示区域的高度。
- `sandbox`：设置嵌入的网页的权限，详见下文。
- `importance`：浏览器下载嵌入的网页的优先级，可以设置三个值。`high`表示高优先级，`low`表示低优先级，`auto`表示由浏览器自行决定。
- `name`：内嵌窗口的名称，可以用于`<a>`、`<form>`、`<base>`的`target`属性。
- `referrerpolicy`：请求嵌入网页时，HTTP 请求的`Referer`字段的设置。参见`<a>`标签的介绍。

## sandbox 属性

嵌入的网页默认具有正常权限，比如执行脚本、提交表单、弹出窗口等。如果嵌入的网页是其他网站的页面，你不了解对方会执行什么操作，因此就存在安全风险。为了限制`<iframe>`的风险，HTML 提供了`sandbox`属性，允许设置嵌入的网页的权限，等同于提供了一个隔离层，即“沙箱”。

`sandbox`可以当作布尔属性使用，表示打开所有限制。

```html
<iframe src="https://www.example.com" sandbox>
</iframe>
```

`sandbox`属性可以设置具体的值，表示逐项打开限制。未设置某一项，就表示不具有该权限。

- `allow-forms`：允许提交表单。
- `allow-modals`：允许提示框，即允许执行`window.alert()`等会产生弹出提示框的 JavaScript 方法。
- `allow-popups`：允许嵌入的网页使用`window.open()`方法弹出窗口。
- `allow-popups-to-escape-sandbox`：允许弹出窗口不受沙箱的限制。
- `allow-orientation-lock`：允许嵌入的网页用脚本锁定屏幕的方向，即横屏或竖屏。
- `allow-pointer-lock`：允许嵌入的网页使用 Pointer Lock API，锁定鼠标的移动。
- `allow-presentation`：允许嵌入的网页使用 Presentation API。
- `allow-same-origin`：不打开该项限制，将使得所有加载的网页都视为跨域。
- `allow-scripts`：允许嵌入的网页运行脚本（但不创建弹出窗口）。
- `allow-storage-access-by-user-activation`：`sandbox`属性同时设置了这个值和`allow-same-origin`的情况下，允许`<iframe>`嵌入的第三方网页通过用户发起`document.requestStorageAccess()`请求，经由 Storage Access API 访问父窗口的 Cookie。
- `allow-top-navigation`：允许嵌入的网页对顶级窗口进行导航。
- `allow-top-navigation-by-user-activation`：允许嵌入的网页对顶级窗口进行导航，但必须由用户激活。
- `allow-downloads-without-user-activation`：允许在没有用户激活的情况下，嵌入的网页启动下载。

注意，不要同时设置`allow-scripts`和`allow-same-origin`属性，这将使得嵌入的网页可以改变或删除`sandbox`属性。

## loading 属性

`<iframe>`指定的网页会立即加载，有时这不是希望的行为。`<iframe>`滚动进入视口以后再加载，这样会比较节省带宽。

`loading`属性可以触发`<iframe>`网页的懒加载。该属性可以取以下三个值。

- `auto`：浏览器的默认行为，与不使用`loading`属性效果相同。
- `lazy`：`<iframe>`的懒加载，即将滚动进入视口时开始加载。
- `eager`：立即加载资源，无论在页面上的位置如何。

```html
<iframe src="https://example.com" loading="lazy"></iframe>
```

上面代码会启用`<iframe>`的懒加载。

有一点需要注意，如果`<iframe>`是隐藏的，则`loading`属性无效，将会立即加载。只要满足以下任一个条件，Chrome 浏览器就会认为`<iframe>`是隐藏的。

> - `<iframe>`的宽度和高度为4像素或更小。
> - 样式设为`display: none`或`visibility: hidden`。
> - 使用定位坐标为负`X`或负`Y`，将`<iframe`>放置在屏幕外。

