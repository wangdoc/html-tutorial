# <link>

## 简介

`<link>`标签主要用于将当前网页与相关的外部资源联系起来，通常放在`<head>`元素里面。最常见的用途就是加载 CSS 样式表。

```html
<link rel="stylesheet" type="text/css" href="theme.css">
```

上面代码为网页加载样式表`theme.css`。

除了默认样式表，网页还可以加载替代样式表，即默认不生效、需要用户手动切换的样式表。

```html
<link href="default.css" rel="stylesheet" title="Default Style">
<link href="fancy.css" rel="alternate stylesheet" title="Fancy">
<link href="basic.css" rel="alternate stylesheet" title="Basic">
```

上面代码中，`default.css`是默认样式表，默认就会生效。`fancy.css`和`basic.css`是替换样式表（`rel="alternate stylesheet"`），默认不生效。`title`属性在这里是必需的，用来在浏览器菜单里面列出这些样式表的名字，供用户选择，以替代默认样式表。

`<link>`还可以加载网站的 favicon 图标文件。

```html
<link rel="icon" href="/favicon.ico" type="image/x-icon">
```

手机访问时，网站通常需要提供不同分辨率的图标文件。

```html
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="favicon114.png">
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="favicon72.png">
```

上面代码指定 iPhone 设备需要的114像素和72像素的图标。

`<link>`也用于提供文档的相关链接，比如下面是给出文档的 RSS Feed 地址。

```html
<link rel="alternate" type="application/atom+xml" href="/blog/news/atom">
```

## href 属性

`href`属性表示`<link>`标签所链接的资源。

## rel 属性

`rel`属性表示外部资源与当前文档之间的关系，是`<link>`标签的必需属性，可以视为对`href`属性所链接资源的说明。

它可以但不限于取以下值。

- `alternate`：文档的另一种表现形式的链接，比如打印版。
- `author`：文档作者的链接。
- `dns-prefetch`：要求浏览器提前执行指定网址的 DNS 查询。
- `help`：帮助文档的链接。
- `icon`：加载文档的图标文件。
- `license`：许可证链接。
- `next`：系列文档下一篇的链接。
- `pingback`：接收当前文档 pingback 请求的网址。
- `preconnect`：要求浏览器提前与给定服务器，建立 HTTP 连接。
- `prefetch`：要求浏览器提前下载并缓存指定资源，供下一个页面使用。它的优先级较低，浏览器可以不下载。
- `preload`：要求浏览器提前下载并缓存指定资源，当前页面稍后就会用到。它的优先级较高，浏览器必须立即下载。
- `prerender`：要求浏览器提前渲染指定链接。这样的话，用户稍后打开该链接，就会立刻显示，感觉非常快。
- `prev`：表示当前文档是系列文档的一篇，这里给出上一篇文档的链接。
- `search`：提供当前网页的搜索链接。
- `stylesheet`：加载一张样式表。

下面是一些示例。

```html
<!-- 作者信息 -->
<link rel="author" href="humans.txt">

<!-- 版权信息 -->
<link rel="license" href="copyright.html">

<!-- 另一个语言的版本 -->
<link rel="alternate" href="https://es.example.com/" hreflang="es">

<!-- 联系方式 -->
<link rel="me" href="https://google.com/profiles/someone" type="text/html">
<link rel="me" href="mailto:name@example.com">
<link rel="me" href="sms:+15035550125">

<!-- 历史资料 -->
<link rel="archives" href="http://example.com/archives/">

<!-- 目录 -->
<link rel="index" href="http://example.com/article/">

<!-- 导航 -->
<link rel="first" href="http://example.com/article/">
<link rel="last" href="http://example.com/article/?page=42">
<link rel="prev" href="http://example.com/article/?page=1">
<link rel="next" href="http://example.com/article/?page=3">
```

## hreflang 属性

`hreflang`属性用来表示`href`属性链接资源的所用语言，通常指当前页面的其他语言版本。

```html
<link href="https://example.com/de" rel="alternate" hreflang="de" />
```

上面示例中，`hreflang`表示`href`属性所链接页面使用德语，即当前页面的德语版本。

如果一个页面有多个语言的版本，`hreflang`属性可以设为`x-default`，表示哪一个页面是默认版本。

```html
<link href="https://example.com" rel="alternate" hreflang="x-default" />
<link href="https://example.com/de" rel="alternate" hreflang="de" />
```

上面示例中，`hreflang`设为`x-default`表示该页面为默认版本。

## 资源的预加载

某些情况下，你需要浏览器预加载某些资源，也就是先把资源缓存下来，等到使用的时候，就不用再从网上下载了，立即就能使用。预处理指令可以做到这一点。

预加载主要有下面五种类型。

### `<link rel="preload">`

`<link rel="preload">`告诉浏览器尽快下载并缓存资源（如脚本或样式表），该指令优先级较高，浏览器肯定会执行。当加载页面几秒钟后需要该资源时，它会很有用。下载后，浏览器不会对资源执行任何操作，脚本未执行，样式表未应用。它只是缓存，当其他东西需要它时，它立即可用。

```html
<link rel="preload" href="image.png" as="image">
```

`rel="preload"`除了优先级较高，还有两个优点：一是允许指定预加载资源的类型，二是允许`onload`事件的回调函数。下面是`rel="preload"`配合`as`属性，告诉浏览器预处理资源的类型，以便正确处理。

```html
<link rel="preload" href="style.css" as="style">
<link rel="preload" href="main.js" as="script">
```

上面代码要求浏览器提前下载并缓存`style.css`和`main.js`。

`as`属性指定加载资源的类型，它的值一般有下面几种。

- "script"
- "style"
- "image"
- "media"
- "document"

如果不指定`as`属性，或者它的值是浏览器不认识的，那么浏览器会以较低的优先级下载这个资源。

有时还需要`type`属性，进一步明确 MIME 类型。

```html
<link rel="preload" href="sintel-short.mp4" as="video" type="video/mp4">
```

上面代码要求浏览器提前下载视频文件，并且说明这是 MP4 编码。

下面是预下载字体文件的例子。

```html
<link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin>
```

注意，所有预下载的资源，只是下载到浏览器的缓存，并没有执行。如果希望资源预下载后立刻执行，可以参考下面的写法。

```html
<link rel="preload" as="style" href="async_style.css" onload="this.rel='stylesheet'">
```

上面代码中，`onload`指定的回调函数会在脚本下载完成后执行，立即插入页面。

### `<link rel="prefetch">`

`<link rel="prefetch">`的使用场合是，如果后续的页面需要某个资源，并且希望预加载该资源，以便加速页面渲染。该指令不是强制性的，优先级较低，浏览器不一定会执行。这意味着，浏览器可以不下载该资源，比如连接速度很慢时。

```html
<link rel="prefetch" href="https://www.example.com/">
```

### `<link rel="preconnect">`

`<link rel="preconnect">`要求浏览器提前与某个域名建立 TCP 连接。当你知道，很快就会请求该域名时，这会很有帮助。

```html
<link rel="preconnect" href="https://www.example.com/">
```

### `<link rel="dns-prefetch">`

`<link rel="dns-prefetch">`要求浏览器提前执行某个域名的 DNS 解析。

```html
<link rel="dns-prefetch" href="//example.com/">
```

### `<link rel="prerender">`

`<link rel="prerender">`要求浏览器加载某个网页，并且提前渲染它。用户点击指向该网页的链接时，就会立即呈现该页面。如果确定用户下一步会访问该页面，这会很有帮助。

```html
<link rel="prerender" href="http://example.com/">
```

## media 属性

`media`属性给出外部资源生效的媒介条件。

```html
<link href="print.css" rel="stylesheet" media="print">
<link href="mobile.css" rel="stylesheet" media="screen and (max-width: 600px)">
```

上面代码中，打印时加载`print.css`，移动设备访问时（设备宽度小于600像素）加载`mobile.css`。

下面是使用`media`属性实现条件加载的例子。

```html
<link rel="preload" as="image" href="map.png" media="(max-width: 600px)">
<link rel="preload" as="script" href="map.js" media="(min-width: 601px)">
```

上面代码中，如果屏幕宽度在600像素以下，则只加载第一个资源，否则就加载第二个资源。

## 其他属性

`<link>`标签的其他属性如下。

- `crossorigin`：加载外部资源的跨域设置。
- `href`：外部资源的网址。
- `referrerpolicy`：加载时`Referer`头信息字段的处理方法。
- `as`：`rel="preload"`或`rel="prefetch"`时，设置外部资源的类型。
- `type`：外部资源的 MIME 类型，目前仅用于`rel="preload"`或`rel="prefetch"`的情况。
- `title`：加载样式表时，用来标识样式表的名称。
- `sizes`：用来声明图标文件的尺寸，比如加载苹果手机的图标文件。

