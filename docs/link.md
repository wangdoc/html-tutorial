# 链接

链接是互联网的核心。它允许用户在页面上，从一个网址跳转到另一个网址，从而把所有资源联系在一起。

URL 是链接指向的地址。链接不仅可以指向另一个网页，也可以指向文本、图像、文件等资源。可以这样说，所有互联网上的资源，都可以通过链接访问。

## `<a>`

链接通过`<a>`标签表示，下面就是一个典型的链接。

```html
这是一个<a href="https://www.example.com/">示例</a>。
```

上面代码在浏览器中，就会显示成一个可以点击的链接。用户点击以后，就会跳转到指定的网址（上例是`www.example.com`）。

`<a>`标签内部不仅可以放置文字，也可以放置其他元素，比如段落、图像、多媒体等等。

```html
<a href="https://www.example.com/">
  <img src="https://www.example.com/foo.jpg">
</a>
```

上面代码中，`<a>`标签内部就是一个图像。用户点击图像，就会跳转到指定网址。

`<a>`标签有如下属性。

**（1）href**

`href`属性给出链接指向的网址。它的值应该是一个 URL 或者 URL 的片断。

上文已经给出了完整 URL 的例子，下面是一个 URL 片断的例子。URL 片断通常是`#`加上锚点的名字。

```html
<a href="#demo">示例</a>
```

上面代码点击后，浏览器会自动滚动到，当前页面里面`demo`锚点所在的位置。

**（2）hreflang**

`hreflang`属性给出链接指向的网址所使用的语言，纯粹是提示性的，没有实际功能。

```html
<a
  href="https://www.example.com"
  hreflang="en"
>示例网址</a>
```

上面代码表明，`href`属性指向的网址的语言是英语。

该属性的值跟通用的`lang`属性是一样的，语言的代码名可以参考《属性》一章的`lang`属性的介绍。

**（3）title**

`title`属性给出链接的说明信息。鼠标悬停在链接上方时，浏览器会将这个属性的值，以提示块的形式显示出来。

```html
<a
  href="https://www.example.com/"
  title="链接的说明信息"
>示例</a>。
```

**（4）target**

`target`属性指定如何展示打开的链接。它可以是窗口（窗口）、Tab（标签）和框架的名字。

```html
<p><a href="http://foo.com" target="test">foo.com</a></p>
<p><a href="http://bar.com" target="test">bar.com</a></p>
```

上面代码中，两个链接都在名叫`test`的窗口打开。首先点击`foo.com`，浏览器发现没有叫做`test`的窗口，就新建一个窗口，起名为`test`，在该窗口打开`foo.com`。然后，用户又点击`bar.com`，由于已经存在`test`窗口，浏览器就在该窗口打开`bar.com`，取代里面已经打开的`foo.com`。

`target`属性也可以是以下四个关键字之一。

- `_self`：当前窗口打开，这是默认值。
- `_blank`：新窗口打开。
- `_parent`：上层窗口打开，这通常用于从父窗口打开的子窗口，或者框架里面的子窗口。如果当前窗口没有上层窗口，这个值等同于`_self`。
- `_top`：顶层窗口打开。如果当前窗口就是上层窗口，这个值等同于`_self`。

```html
<a
  href="https://www.example.com"
  target="_blank"
>示例链接</a>
```

上面代码点击后，浏览器会新建一个窗口，在该窗口打开链接。

注意，使用`target`属性的时候，最好跟`rel="noreferrer"`一起使用，这样可以避免安全风险。

**（5）rel**

`rel`属性说明链接与当前页面的关系。

```html
<a href="help.html" rel="help">帮助</a>
```

上面代码的`rel`属性，说明链接是当前页面的帮助文档。

`<a>`元素的`rel`属性的取值，有以下这些。

- alternate：当前文档的另一种形式，比如翻译。
- author：作者链接。
- bookmark：用作书签的永久地址。
- external：当前文档的外部参考文档。
- help：帮助链接。
- license：许可证链接。
- next：系列文档的下一篇。
- nofollow：告诉搜索引擎忽略该链接，主要用于用户提交的内容，防止有人企图通过添加链接，提高该链接的搜索排名。
- noreferrer：告诉浏览器打开链接时，不要将当前网址作为 HTTP 头信息的`Referer`字段发送出去，这样可以隐藏点击的来源。
- noopener：告诉浏览器打开链接时，不让链接窗口通过 JavaScript 的`window.opener`属性引用原始窗口，这样就提高了安全性。
- prev：系列文档的上一篇。
- search：文档的搜索链接。
- tag：文档的标签链接。

**（6）referrerpolicy**

`referrerpolicy`属性用于精确设定点击链接时，浏览器发送 HTTP 头信息的`Referer`字段的行为。

该属性可以取下面八个值：`no-referrer`、`no-referrer-when-downgrade`、`origin`、`origin-when-cross-origin`、`unsafe-url`、`same-origin`、`strict-origin`、`strict-origin-when-cross-origin`。

其中，`no-referrer`表示不发送`Referer`字段，`same-origin`表示同源时才发送`Referer`字段，`origin`表示只发送源信息（协议+域名+端口）。其他几项的解释，请查阅 HTTP 文档。

**（7）ping**

`ping`属性指定一个网址，用户点击的时候，会向该网址发出一个 POST 请求，通常用于跟踪用户的行为。

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

注意，如果链接点击后，服务器的 HTTP 回应设置了头信息`Content-Disposition`，并且头信息的值与`download`属性不一致，那么头信息优先，下载时将显示其设置的文件名。

`download`属性还有一个用途，就是有些地址不是真实网址，而是数据网址，比如`data:`开头的网址，直接描述了数据内容。

```html
<a href="data:,Hello%2C%20World!">点击</a>
```

上面链接点击后，会打开一个虚拟网页，上面显示`Hello World!`。这个虚拟网页的内容，都在数据网址里面指定了。

这时，`download`属性可以用于为虚拟网址，指定下载的文件名。

```html
<a
  href="data:,Hello%2C%20World!"
  download="hello.txt"
>点击</a>
```

上面链接点击后，下载的`hello.txt`文件内容就是“hello.txt”。

## 邮件链接

链接也可以指向一个邮件地址，使用`mailto`协议。用户点击后，浏览器会打开本机默认的邮件程序，让用户向指定的地址发送邮件。

```html
<a href="mailto:contact@example.com">联系我们</a>
```

上面代码中，链接就指向邮件地址。点击后，浏览器会打开一个邮件地址，让你可以向`contact@example.com`发送邮件。

除了邮箱，邮件协议还允许指定其他几个邮件要素。

- subject：主题
- cc：抄送
- bcc：密送
- body：邮件内容

指定方法是将这些邮件要素，以查询字符串的方式，附加在邮箱地址后面。

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

`<link>`标签主要用于将当前网页与相关的外部资源联系起来，通常放在`<head>`元素里面。最常见的用途就是加载样式表。

```html
<link rel="stylesheet" type="text/css" href="theme.css">
```

上面代码为网页加载样式表`theme.css`。

除了默认样式表，网页还可以加载替代样式表，即默认情况不生效、需要用户手动切换的样式表。

```html
<link href="default.css" rel="stylesheet" title="Default Style">
<link href="fancy.css" rel="alternate stylesheet" title="Fancy">
<link href="basic.css" rel="alternate stylesheet" title="Basic">
```

上面代码中，`default.css`是默认样式表，默认就会生效。`fancy.css`和`basic.css`是替换样式表（`rel="alternate stylesheet"`），默认情况下不生效。`title`属性这时是必需的，会列在浏览器菜单里面，供用户选择，以替代默认样式表。

`<link>`还可以加载网站的 favicon 图标文件。

```html
<link rel="icon" href="/favicon.ico" type="image/x-icon">
```

手机访问时，网站通常需要提供不同分辨率使用的图标文件。

```html
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="favicon114.png">
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="favicon72.png">
```

上面代码指定 iPhone 设备需要的114像素和72像素的图标。

`<link>`也用于提供文档的相关链接，比如下面是给出文档的 RSS Feed 地址，具体解释见后文。

```html
<link rel="alternate" type="application/atom+xml" href="/blog/news/atom">
```

### media 属性

`media`属性给出外部资源生效的媒介条件。

```html
<link href="print.css" rel="stylesheet" media="print">
<link href="mobile.css" rel="stylesheet" media="screen and (max-width: 600px)">
```

上面代码中，打印时加载`print.css`，移动设备访问时（设备宽度小于600像素）加载`mobile.css`。

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

下面是`rel="preload"`的一些例子。

```html
<link rel="preload" href="style.css" as="style">
<link rel="preload" href="main.js" as="script">
```

上面代码要求浏览器提前下载并缓存`style.css`和`main.js`。

配合使用的`as`属性，告诉浏览器这些资源的类型，以便正确处理。

有时还需要`type`属性，进一步明确 MIME 类型。

```html
<link rel="preload" href="sintel-short.mp4" as="video" type="video/mp4">
```

上面代码要求浏览器提前下载视频文件，并且说明这是 MP4 编码。

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

`<script>`用于加载脚本代码，目前主要是 JavaScript 代码。

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

`type`属性给出脚本的类型，默认是 JavaScript 代码，所以可省略。

```html
<script type="text/javascript" src="javascript.js"></script>
```

`type`属性也可以设成`module`，表示这是一个 ES6 模块，不是传统脚本。

```html
<script type="module" src="main.js"></script>
```

对于那些不支持 ES6 模块的浏览器，可以设置`nomodule`属性。支持 ES6 模块的浏览器，就会不加载指定的脚本。这个属性通常与`type="module"`配合使用，作为老式浏览器的回退方案。

```html
<script type="module" src="main.js"></script>
<script nomodule src="fallback.js"></script>
```

`<script>`还有一些其他属性，大部分跟 JavaScript 语言有关，可以参考相关的 JavaScript 教程。

- `async`：该属性指定 JavaScript 代码为异步执行，不是造成阻塞效果，JavaScript 代码默认是同步执行。
- `defer`：该属性指定 JavaScript 代码不是立即执行，而是页面解析完成后执行。
- `crossorigin`：如果采用这个属性，就会采用跨域的方式加载外部脚本，即 HTTP 请求的头信息会加上`origin`字段。
- `integrity`：给出外部脚本的哈希值，防止脚本被篡改。只有哈希值相符的外部脚本，才会执行。
- `nonce`：一个密码随机数，由服务器在 HTTP 头信息里面给出，每次加载脚本都不一样。它相当于给出了内嵌脚本的白名单，只有在白名单内的脚本才能执行。
- `referrerpolicy`：HTTP 请求的`Referer`字段的处理方法。

