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

只使用`#`，不加锚点名，也是可以的。点击后，浏览器会滚动到页面顶部，这也是常见做法。

```html
<a href="#">回到顶部</a>
```

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

**（）ping**

`ping`属性指定一个网址，用户点击的时候，会向该网址发出一个 POST 请求，通常用于跟踪用户的行为。

**（4）type**

`type`属性给出链接 URL 的 MIME 类型，比如到底是网页，还是图像或文件。它也是纯粹提示性的属性，没有实际功能。

```html
<a
  href="smile.jpg"
  type="image/jpeg"
>示例图片</a>
```

上面代码中，`type`属性提示这是一张图片。

**（5）download**

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

