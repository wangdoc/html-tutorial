# 链接标签

链接（hyperlink）是互联网的核心。它允许用户在页面上，从一个网址跳转到另一个网址，从而把所有资源联系在一起。

URL 是链接指向的地址。链接不仅可以指向另一个网页，也可以指向文本、图像、文件等资源。可以这样说，所有互联网上的资源，都可以通过链接访问。

## `<a>`

链接通过`<a>`标签表示，用户点击后，浏览器会跳转到指定的网址。下面就是一个典型的链接。

```html
<a href="https://wikipedia.org/">维基百科</a>
```

上面代码就定义了一个超级链接。浏览器显示“维基百科”，文字下面默认会有下划线，表示这是一个链接。用户点击后，浏览器跳转到`href`属性指定的网址。

`<a>`标签内部不仅可以放置文字，也可以放置其他元素，比如段落、图像、多媒体等等。

```html
<a href="https://www.example.com/">
  <img src="https://www.example.com/foo.jpg">
</a>
```

上面代码中，`<a>`标签内部就是一个图像。用户点击图像，就会跳转到指定网址。

`<a>`标签有如下属性。

**（1）href**

`href`属性给出链接指向的网址。它的值应该是一个 URL 或者锚点。

上文已经给出了完整 URL 的例子，下面是锚点的例子。

```html
<a href="#demo">示例</a>
```

上面代码中，`href`属性的值是`#`加上锚点名称。点击后，浏览器会自动滚动，停在当前页面里面`demo`锚点所在的位置。

**（2）hreflang**

`hreflang`属性给出链接指向的网址所使用的语言，纯粹是提示性的，没有实际功能。

```html
<a
  href="https://www.example.com"
  hreflang="en"
>示例网址</a>
```

上面代码表明，`href`属性指向的网址的语言是英语。

该属性的值跟通用属性`lang`一样，语言代码可以参考《属性》一章的`lang`属性的介绍。

**（3）title**

`title`属性给出链接的说明信息。鼠标悬停在链接上方时，浏览器会将这个属性的值，以提示块的形式显示出来。

```html
<a
  href="https://www.example.com/"
  title="hello"
>示例</a>。
```

上面代码中，用户鼠标停留在链接上面，会出现文字提示`hello`。

**（4）target**

`target`属性指定如何展示打开的链接。它可以是在指定的窗口打开，也可以在`<iframe>`里面打开。

```html
<p><a href="http://foo.com" target="test">foo</a></p>
<p><a href="http://bar.com" target="test">bar</a></p>
```

上面代码中，两个链接都在名叫`test`的窗口打开。首先点击链接`foo`，浏览器发现没有叫做`test`的窗口，就新建一个窗口，起名为`test`，在该窗口打开`foo.com`。然后，用户又点击链接`bar`，由于已经存在`test`窗口，浏览器就在该窗口打开`bar.com`，取代里面已经打开的`foo.com`。

`target`属性的值也可以是以下四个关键字之一。

- `_self`：当前窗口打开，这是默认值。
- `_blank`：新窗口打开。
- `_parent`：上层窗口打开，这通常用于从父窗口打开的子窗口，或者`<iframe>`里面的链接。如果当前窗口没有上层窗口，这个值等同于`_self`。
- `_top`：顶层窗口打开。如果当前窗口就是顶层窗口，这个值等同于`_self`。

```html
<a
  href="https://www.example.com"
  target="_blank"
>示例链接</a>
```

上面代码点击后，浏览器会新建一个窗口，在该窗口打开链接，并且新窗口没有名字。

注意，使用`target`属性的时候，最好跟`rel="noreferrer"`一起使用，这样可以避免安全风险。

**（5）rel**

`rel`属性说明链接与当前页面的关系。

```html
<a href="help.html" rel="help">帮助</a>
```

上面代码的`rel`属性，说明链接是当前页面的帮助文档。

下面是一些常见的`rel`属性的值。

- `alternate`：当前文档的另一种形式，比如翻译。
- `author`：作者链接。
- `bookmark`：用作书签的永久地址。
- `external`：当前文档的外部参考文档。
- `help`：帮助链接。
- `license`：许可证链接。
- `next`：系列文档的下一篇。
- `nofollow`：告诉搜索引擎忽略该链接，主要用于用户提交的内容，防止有人企图通过添加链接，提高该链接的搜索排名。
- `noreferrer`：告诉浏览器打开链接时，不要将当前网址作为 HTTP 头信息的`Referer`字段发送出去，这样可以隐藏点击的来源。
- `noopener`：告诉浏览器打开链接时，不让链接窗口通过 JavaScript 的`window.opener`属性引用原始窗口，这样就提高了安全性。
- `prev`：系列文档的上一篇。
- `search`：文档的搜索链接。
- `tag`：文档的标签链接。

**（6）referrerpolicy**

`referrerpolicy`属性用于精确设定点击链接时，浏览器发送 HTTP 头信息的`Referer`字段的行为。

该属性可以取下面八个值：`no-referrer`、`no-referrer-when-downgrade`、`origin`、`origin-when-cross-origin`、`unsafe-url`、`same-origin`、`strict-origin`、`strict-origin-when-cross-origin`。

其中，`no-referrer`表示不发送`Referer`字段，`same-origin`表示同源时才发送`Referer`字段，`origin`表示只发送源信息（协议+域名+端口）。其他几项的解释，请查阅 HTTP 文档。

**（7）ping**

`ping`属性指定一个网址，用户点击的时候，会向该网址发出一个 POST 请求，通常用于跟踪用户的行为。

```html
<a href="http://localhost:3000/other" ping="http://localhost:3000/log">
  Go to Other Page
</a>
```

上面示例中，用户点击链接时，除了发生跳转，还会向`http://localhost:3000/log`发送一个 POST 请求。服务端收到这个请求以后，就会知道用户点击了这个链接。

这个请求的 HTTP 标头，包含了`ping-from`属性（点击行为发生的页面）和`ping-to`属性（`href`属性所指向的页面）。

```http
headers: {
  'ping-from': 'http://localhost:3000/',
  'ping-to': 'http://localhost:3000/other'
  'content-type': 'text/ping'
  // ...other headers
},
```

注意，`ping`属性只对链接有效，对其他的交互行为无效，比如按钮点击或表单提交。另外，Firefox 浏览器不支持该属性。并且，也无法让它发送任何的自定义数据。

**（8）type**

`type`属性给出链接 URL 的 MIME 类型，比如到底是网页，还是图像或文件。它也是纯粹提示性的属性，没有实际功能。

```html
<a
  href="smile.jpg"
  type="image/jpeg"
>示例图片</a>
```

上面代码中，`type`属性提示这是一张图片。

**（9）download**

`download`属性表明当前链接用于下载，而不是跳转到另一个 URL。

```html
<a href="demo.txt" download>下载</a>
```

上面代码点击后，会出现下载对话框。

注意，`download`属性只在链接与网址同源时，才会生效。也就是说，链接应该与网址属于同一个网站。

如果`download`属性设置了值，那么这个值就是下载的文件名。

```html
<a
  href="foo.exe"
  download="bar.exe"
>点击下载</a>
```

上面代码中，下载文件的原始文件名是`foo.exe`。点击后，下载对话框提示的文件名是`bar.exe`。

注意，如果链接点击后，服务器的 HTTP 回应的头信息设置了`Content-Disposition`字段，并且该字段的值与`download`属性不一致，那么该字段优先，下载时将显示其设置的文件名。

`download`属性还有一个用途，就是有些地址不是真实网址，而是数据网址，比如`data:`开头的网址。这时，`download`属性可以为虚拟网址指定下载的文件名。

```html
<a href="data:,Hello%2C%20World!">点击</a>
```

上面链接点击后，会打开一个虚拟网页，上面显示`Hello World!`。


```html
<a
  href="data:,Hello%2C%20World!"
  download="hello.txt"
>点击</a>
```

上面链接点击后，下载的`hello.txt`文件内容就是“Hello, World!”。

## 邮件链接

链接也可以指向一个邮件地址，使用`mailto`协议。用户点击后，浏览器会打开本机默认的邮件程序，让用户向指定的地址发送邮件。

```html
<a href="mailto:contact@example.com">联系我们</a>
```

上面代码中，链接就指向邮件地址。点击后，浏览器会打开一个邮件地址，让你可以向`contact@example.com`发送邮件。

除了邮箱，邮件协议还允许指定其他几个邮件要素。

- `subject`：主题
- `cc`：抄送
- `bcc`：密送
- `body`：邮件内容

使用方法是将这些邮件要素，以查询字符串的方式，附加在邮箱地址后面。

```html
<a
  href="mailto:foo@bar.com?cc=test@test.com&subject=The%20subject&body=The%20body"
>发送邮件</a>
```

上面代码中，邮件链接里面不仅包含了邮箱地址，还包含了`cc`、`subject`、`body`等邮件要素。这些要素的值需要经过 URL 转义，比如空格转成`%20`。

不指定邮箱也是允许的，就像下面这样。这时用户自己在邮件程序里面，填写想要发送的邮箱，通常用于邮件分享网页。

```html
<a href="mailto:">告诉朋友</a>
```

## 电话链接

如果是手机浏览的页面，还可以使用`tel`协议，创建电话链接。用户点击该链接，会唤起电话，可以进行拨号。

```html
<a href="tel:13312345678">13312345678</a>
```

上面代码在手机中，点击链接会唤起拨号界面，可以直接拨打指定号码。

## `<link>`

### 基本用法

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

### rel 属性

`rel`属性表示外部资源与当前文档之间的关系，是`<link>`标签的必需属性。它可以但不限于取以下值。

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

### 资源的预加载

某些情况下，你需要浏览器预加载某些资源，也就是先把资源缓存下来，等到使用的时候，就不用再从网上下载了，立即就能使用。预处理指令可以做到这一点。

预加载主要有下面五种类型。

（1）`<link rel="preload">`

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

（2）`<link rel="prefetch">`

`<link rel="prefetch">`的使用场合是，如果后续的页面需要某个资源，并且希望预加载该资源，以便加速页面渲染。该指令不是强制性的，优先级较低，浏览器不一定会执行。这意味着，浏览器可以不下载该资源，比如连接速度很慢时。

```html
<link rel="prefetch" href="https://www.example.com/">
```

（3）`<link rel="preconnect">`

`<link rel="preconnect">`要求浏览器提前与某个域名建立 TCP 连接。当你知道，很快就会请求该域名时，这会很有帮助。

```html
<link rel="preconnect" href="https://www.example.com/">
```

（4）`<link rel="dns-prefetch">`

`<link rel="dns-prefetch">`要求浏览器提前执行某个域名的 DNS 解析。

```html
<link rel="dns-prefetch" href="//example.com/">
```

（5）`<link rel="prerender">`

`<link rel="prerender">`要求浏览器加载某个网页，并且提前渲染它。用户点击指向该网页的链接时，就会立即呈现该页面。如果确定用户下一步会访问该页面，这会很有帮助。

```html
<link rel="prerender" href="http://example.com/">
```

### media 属性

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

### 其他属性

`<link>`标签的其他属性如下。

- `crossorigin`：加载外部资源的跨域设置。
- `href`：外部资源的网址。
- `referrerpolicy`：加载时`Referer`头信息字段的处理方法。
- `as`：`rel="preload"`或`rel="prefetch"`时，设置外部资源的类型。
- `type`：外部资源的 MIME 类型，目前仅用于`rel="preload"`或`rel="prefetch"`的情况。
- `title`：加载样式表时，用来标识样式表的名称。
- `sizes`：用来声明图标文件的尺寸，比如加载苹果手机的图标文件。

## `<script>`

`<script>`用于加载脚本代码，目前主要是加载 JavaScript 代码。

```html
<script>
console.log('hello world');
</script>
```

上面代码嵌入网页，会立即执行。

`<script>`也可以加载外部脚本，`src`属性给出外部脚本的地址。

```html
<script src="javascript.js"></script>
```

上面代码会加载`javascript.js`脚本文件，并执行。

`type`属性给出脚本的类型，默认是 JavaScript 代码，所以可省略。完整的写法其实是下面这样。

```html
<script type="text/javascript" src="javascript.js"></script>
```

`type`属性也可以设成`module`，表示这是一个 ES6 模块，不是传统脚本。

```html
<script type="module" src="main.js"></script>
```

对于那些不支持 ES6 模块的浏览器，可以设置`nomodule`属性。支持 ES6 模块的浏览器，会不加载指定的脚本。这个属性通常与`type="module"`配合使用，作为老式浏览器的回退方案。

```html
<script type="module" src="main.js"></script>
<script nomodule src="fallback.js"></script>
```

`<script>`还有下面一些其他属性，大部分跟 JavaScript 语言有关，可以参考相关的 JavaScript 教程。

- `async`：该属性指定 JavaScript 代码为异步执行，不是造成阻塞效果，JavaScript 代码默认是同步执行。
- `defer`：该属性指定 JavaScript 代码不是立即执行，而是页面解析完成后执行。
- `crossorigin`：如果采用这个属性，就会采用跨域的方式加载外部脚本，即 HTTP 请求的头信息会加上`origin`字段。
- `integrity`：给出外部脚本的哈希值，防止脚本被篡改。只有哈希值相符的外部脚本，才会执行。
- `nonce`：一个密码随机数，由服务器在 HTTP 头信息里面给出，每次加载脚本都不一样。它相当于给出了内嵌脚本的白名单，只有在白名单内的脚本才能执行。
- `referrerpolicy`：HTTP 请求的`Referer`字段的处理方法。

## `<noscript>`

`<noscript>`标签用于浏览器不支持或关闭 JavaScript 时，所要显示的内容。用户关闭 JavaScript 可能是为了节省带宽，以延长手机电池寿命，或者为了防止追踪，保护隐私。

```html
<noscript>
  您的浏览器不能执行 JavaScript 语言，页面无法正常显示。
</noscript>
```

上面这段代码，只有浏览器不能执行 JavaScript 代码时才会显示，否则就不会显示。

## 参考链接

- [A free guide to `<head>` elements](https://htmlhead.dev/)

