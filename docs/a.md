# <a>

## 简介

链接（hyperlink）是互联网的核心。它允许用户在页面上，从一个网址跳转到另一个网址，从而把所有资源联系在一起。

`<a>`标签就代表一个可以跳转的链接。它不仅可以跳转到其他页面，也可以跳转到文本、图像、文件等资源，甚至当前页面的某个位置。可以这样说，所有互联网上的资源，都可以通过`<a>`访问。

下面就是一个典型的链接。

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

## 属性

`<a>`标签有如下属性。

### href

`href`属性给出链接指向的网址。它的值应该是一个 URL 或者锚点。

上文已经给出了完整 URL 的例子，下面是锚点的例子。

```html
<a href="#demo">示例</a>
```

上面代码中，`href`属性的值是`#`加上锚点名称。点击后，浏览器会自动滚动，停在当前页面里面`demo`锚点所在的位置。

### hreflang

`hreflang`属性给出链接指向的网址所使用的语言，纯粹是提示性的，没有实际功能，主要供搜索引擎使用。

```html
<a
  href="https://www.example.com"
  hreflang="en"
>示例网址</a>
```

上面代码表明，`href`属性指向的网址的语言是英语。

如果某个资源有多种语言的不同版本，可以将`hreflang`设为`x-default`，表示哪一个链接是默认版本。

```html
<a href="https://example.com" hreflang="x-default">English</a>
<a href="https://example.com/de" hreflang="de">German</a>
```

上面示例中，`hreflang`设为`x-defalut`表示该链接为默认版本。

`hreflang`属性所用的语言代码，跟通用的`lang`属性一样，可以参考《属性》一章的`lang`属性的介绍。

### title

`title`属性给出链接的说明信息。鼠标悬停在链接上方时，浏览器会将这个属性的值，以提示块的形式显示出来。

```html
<a
  href="https://www.example.com/"
  title="hello"
>示例</a>。
```

上面代码中，用户鼠标停留在链接上面，会出现文字提示`hello`。

### target

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

### rel

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

### referrerpolicy

`referrerpolicy`属性用于精确设定点击链接时，浏览器发送 HTTP 头信息的`Referer`字段的行为。

该属性可以取下面八个值：`no-referrer`、`no-referrer-when-downgrade`、`origin`、`origin-when-cross-origin`、`unsafe-url`、`same-origin`、`strict-origin`、`strict-origin-when-cross-origin`。

其中，`no-referrer`表示不发送`Referer`字段，`same-origin`表示同源时才发送`Referer`字段，`origin`表示只发送源信息（协议+域名+端口）。其他几项的解释，请查阅 HTTP 文档。

### ping

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

### type

`type`属性给出链接 URL 的 MIME 类型，比如到底是网页，还是图像或文件。它也是纯粹提示性的属性，没有实际功能。

```html
<a
  href="smile.jpg"
  type="image/jpeg"
>示例图片</a>
```

上面代码中，`type`属性提示这是一张图片。

### download

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

