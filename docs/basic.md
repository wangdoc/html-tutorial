# 基本语法

HTML 是网页的语言，用来定义网页的内容，比如标题、段落、内容。浏览器根据 HTML 代码，渲染出网页。

下面是一个简单的网页 HTML 代码。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>网页标题</title>
</head>
<body>
  <p>Hello World</p>
</body>
</html>
```

你将上面这段代码保存成`hello.html`，然后在浏览器加载这个本地文件，应该就能看到“Hello World”。

HTML 代码由不同的标签构成，标签名放在一对尖括号里面，比如`<title>`和`<p>`。大多数标签都是成对出现的，分成开始标签和结束标签，结束标签在标签名之前加斜杠，比如`<title>`和`</p>`。也有一些标签，没有结束标签，比如上面的`<meta>`标签。

标签的内容就放在开始标签和结束标签之间。

```html
<title>网页标题</title>
```

上面代码中，`<title>`标签的内容就是“网页标题”。

很显然，那些没有结束标签的标签，是没有办法设置内容的。

几乎所有标签，都可以设置属性，放置在标签名之后。

```html
<meta charset="utf-8" />
```

上面代码中，`<meta>`标签有一个`charset`属性，`charset`是属性名，`utf-8`是属性值。

标签是大小写不敏感的，比如`<a>`和`<A>`是同一个标签，`onclick`与`onClick`是同一个属性。

另外，HTML 语言忽略缩进和换行。也就是说，上面的那段代码完全可以写成一行，浏览器照样解析，结果完全一样。网页上面的缩进和换行要靠 CSS 样式和标签来实现。

## doctype

HTML5 的`doctype`非常简单，只要声明`html`即可。

```html
<!doctype html>
```

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


