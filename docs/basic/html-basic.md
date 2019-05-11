# 基本语法

## 概述

HTML 是网页的语言，用来定义网页的结构和内容，比如标题、段落、图像和视频。浏览器根据 HTML 代码，渲染出网页。它是“超文本标记语言”（HyperText Markup Language）的缩写。

下面是一个简单网页的 HTML 代码。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>网页标题</title>
</head>
<body>
  <p>Hello World</p>
</body>
</html>
```

你将上面这段代码保存成`hello.html`，然后在浏览器加载这个本地文件，应该就能看到“Hello World”。

## 基本概念

### 标签

HTML 代码由许许多多不同的标签（tag）构成。

```html
<title>网页标题</title>
```

上面代码中，`<title>`和`</title>`就是一对标签，“网页标题”就是这个标签的内容。

标签名放在一对尖括号里面，比如`<title>`。大多数标签都是成对出现的，分成开始标签和结束标签，结束标签在标签名之前加斜杠，比如`</title>`。但是也有一些标签不是成对使用，而是只有开始标签，没有结束标签，比如上面的`<meta>`标签。

```html
<meta charset="utf-8">
```

标签的内容就放在开始标签和结束标签之间。如果不是成对出现的标签，那么也就不存在标签内容。

标签可以嵌套。

```html
<div><p>hello world</p></div>
```

上面代码中，`<div>`标签内部包含了一个`<p>`标签。

嵌套时，必须保证正确的闭合顺序，不能跨层嵌套，否则会出现意想不到的渲染结果。

```html
<div><p>hello world</div></p>
```

上面代码就是错误的嵌套，闭合顺序不正确。

标签名是大小写不敏感的，比如`<title>`和`<TITLE>`是同一个标签。不过，一般习惯都是使用小写。

另外，HTML 语言忽略缩进和换行。也就是说，下面的写法与上面的写法效果是一样的。

```html
<title>
  网页标题
</title>
```

进一步说，整个网页的 HTML 代码完全可以写成一行，浏览器照样解析，结果完全一样。有时，正式发布网页之前，开发者会把源码压缩成一行，以减少传输的字节数。网页内容的缩进和换行要靠 CSS 样式和特定的标签来实现。

### 元素

有的标签是实义标签，也就是说，标签有对应的实体，即对应 HTML 网页的元素（element）。比如，`<p>`标签对应网页的`p`元素。

嵌套的标签就构成了网页元素的层级关系。

```html
<div><p>hello world</p></div>
```

上面代码中，`div`元素内部包含了一个`p`元素。这时，上层元素称为“父元素”，下层元素称为“子元素”，即`div`是`p`的父元素，`p`是`div`的子元素。

元素分成块级元素（block）和行内元素（inline）两种。块级元素默认占据一个独立的区域，在网页上会自动另起一行，占据 100% 的宽度。

```html
<p>hello</p>
<p>world</p>
```

上面代码中，`p`元素是块级元素，因此浏览器会将内容分成两行显示。

行内元素默认与其他元素在同一行，不占据一个单独的区域。通常用来为某些文字指定特别的样式。

```html
<span>hello</span>
<span>world</span>
```

上面代码中，`span`元素是行内元素，因此浏览器会将内容放在一行显示。

### 属性

属性（attribute）是标签的额外信息，使用空格与标签名和其他属性分隔。

```html
<img src="demo.jpg" width="500">
```

上面代码中，`<img>`标签有两个属性：`src`和`width`。

属性可以用等号指定属性值，比如上例的`demo.jpg`就是`src`的属性值。属性值一般放在双引号里面，这不是必需的，但推荐总是使用双引号。

有些属性是布尔属性，即属性值是一个布尔值，只有“打开”和“关闭”两种情况。这时属性值可以省略，只要添加了属性名，就表示打开该属性。

```html
<input type="text" required>
```

上面代码中，`required`就是`<input>`标签的布尔属性。如果没有这个属性，就表示关闭，否则就是打开。

注意，属性名是大小写不敏感的，`onclick`和`onClick`是同一个属性。

## 网页的基本结构

符合语法标准的网页，应该满足下面的基本结构。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
</head>
<body>
</body>
</html>
```

不管多么复杂的网页，都是从上面这个基本结构衍生出来的。

注意，上面代码的缩进和换行，对于浏览器来说都不重要。上面这样写，只是为了提高可读性。

下面介绍，这个基本结构里面的每一个标签。

### `<doctype>`

网页的第一个标签通常是`<doctype>`，用来表示文档类型，这告诉浏览器如何处理网页。

一般来说，只要像下面这样，简单声明成`html`即可。浏览器就会使用 HTML 的规则处理这个文件。

```html
<!doctype html>
```

这个标签完全采用大写，也很常见。

```html
<!DOCTYPE html>
```

### `<html>`

`<html>`标签是网页的顶层容器。所有网页内容都要放在这个标签内部，都是它的后代标签。一个网页只能有一个`<html>`标签。

该标签有一个`lang`属性，表示网页内容默认的语言。

```html
<html lang="language-code">
```

`lang`属性的值，必须符合 [BCP47](https://www.ietf.org/rfc/bcp/bcp47.txt) 的标准。下面是一些常见的语言代码。

- zh：中文
- zh-Hans：简体中文
- zh-Hant：繁体中文
- en：英语
- en-US：美国英语
- en-GB：英国英语
- es：西班牙语
- fr：法语

### `<head>`

`<head>`标签是一个容器标签，用于放置网页的头部内容。它与页面的渲染不是直接相关，而是用于为渲染结果做准备。

如果网页不包含`<head>`，浏览器会自动创建一个 head 元素。

### `<meta>`

`<meta>`标签用于指定网页的一些元数据。其中最重要的一项，就是网页的编码方式。

```html
<meta charset="utf-8">
```

上面代码声明，网页为`utf-8`编码。虽然可以使用其他的编码方式，但 UTF-8 实际已经足够使用。

注意，声明的编码方式，应该与网页实际的编码方式一致，即声明了`utf-8`，网页就应该使用 UTF-8 编码保存。

### `<title>`

`<title>`标签用于指定网页的标题，会显示在浏览器的标题栏。

搜索引擎显示搜索结果时，也是采用这个标签的内容，给予它很高的权重。所以，`<title>`标签对于网页在搜索引擎的排序，有很大的影响，应该精心安排，反映网页最重要的主题。

`<title>`标签的内部，不能再放置其他标签，只能放置无格式的纯文本。

### `<body>`

`<body>`标签是一个容器标签，用于放置网页的主体内容。浏览器显示的页面内容，就是在这里指定。

## 空格和换行

对于空格，HTML 语言有自己的处理规则。标签内容里面的多个连续空格（包含制表符`\t`），会被浏览器合并成一个。

```html
<p>hello      world</p>
```

上面代码中，`hello`与`world`之间有多个连续空格，浏览器会将它们合并成一个。网页渲染的结果是，`hello`与`world`之间只有一个空格。

浏览器还会将文本里面的换行符（`\n`）和回车符（`\r`），替换成空格。

```html
<p>hello



world
</p>
```

上面代码中，`hello`与`world`之间有多个换行，浏览器会将它们替换成空格，然后再将多个空格合并成一个。网页渲染的结果是，`hello`与`world`之间有一个空格。

这意味着，HTML 源码里面的换行，不会产生换行效果。

## 语义元素

HTML5 引入一系列带有语义的区块，不必再使用`<div>`了。

- `<main>`：主区块
- `<aside>`：副内容
- `<nav>`：导航区块
- `<article>`：内容区块，网页中可以有多个`<article>`，一个`<article>`也可以包含多个`<section>`
- `<section>`：结构区块，一个`<section>`可以包含多个`<article>`
- `<header>`：头部区块
- `<footer>`：尾部区块
- `<figure>`：图片区块
- `<figcaption>`：图片标题区块

