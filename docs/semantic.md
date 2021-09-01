# 网页的语义结构

HTML 标签的名称都带有语义（semantic），使用时应该尽量符合标签的语义，不要用错误语义的标签。语义良好的网页，天然具有良好的结构，对于开发者易读易写，容易维护，也能帮助计算机更好地处理网页内容。

## 含义

HTML 标签的一个重要作用，就是声明网页元素的性质，使得用户只看标签，就能了解这个元素的意义，阅读 HTML 源码就能了解网页的大致结构。这被称为 HTML 的语义原则。

下面就是一个典型的语义结构的网页。

```html
<body>
  <header>页眉</header>
  <main>
    <article>
      <h1>文章标题</h1>
      <p>文章内容</p>
    </article>
  </main>
  <footer>页尾</footer>
</body>
```

只看上面的代码，就可以知道，页面分成页眉（`<header>`）、主体（`<main>`）、页尾（`<footer>`）三个部分。

编写 HTML 网页，第一步就是写出语义结构的网页骨架。

## 常用标签

### `<header>`

`<header>`标签可以用在多个场景，既可以表示整个网页的头部，也可以表示一篇文章或者一个区块的头部。

如果用在网页的头部，就称为“页眉”。网站导航和搜索栏通常会放在`<header>`里面。

```html
<header>
  <h1>公司名称</h1>
  <ul>
    <li><a href="/home">首页</a></li>
    <li><a href="/about">关于</a></li>
    <li><a href="/contact">联系</a></li>
  </ul>
  <form target="/search">
    <input name="q" type="search" />
    <input type="submit" />
  </form>
</header>
```

如果`<header>`用在文章的头部，则可以把文章标题、作者等信息放进去。

```html
<article>
  <header>
    <h2>文章标题</h2>
    <p>张三，发表于2010年1月1日</p>
  </header>
</article>
```

由于`<header>`可以用在多种场景，所以一个页面可能包含多个`<header>`，但是一个具体的场景里面只能包含一个，比如网页的页眉只能有一个。另外，`<header>`里面不能包含另一个`<header>`或`<footer>`。

### `<footer>`

`<footer>`标签表示网页、文章或章节的尾部。如果用于整张网页的尾部，就称为“页尾”，通常包含版权信息或者其他相关信息。

```html
<body>
  <footer>
    <p>© 2018 xxx 公司</p>
  </footer>
</body>
```

上面代码中，版权信息放在`<footer>`里面。

`<footer>`也可以放在文章里面。

```html
<article>
  <header>
    <h1>文章标题</h1>
  </header>
  <footer>
    <p>© 禁止转贴</p>
  </footer>
</article>
```

`<footer>`不能嵌套，即内部不能放置另一个`<footer>`，也不能放置`<header>`。

### `<main>`

`<main>`标签表示页面的主体内容，一个页面只能有一个`<main>`。

```html
<body>
<header>页眉</header>
<main>
  <article>文章</article>
</main>
<aside>侧边栏</aside>
<footer>页尾</footer>
</body>
```

上面代码就是最典型的页面结构。

注意，`<main>`是顶层标签，不能放置在`<header>`、`<footer>`、`<article>`、`<aside>`、`<nav>`等标签之中。

另外，功能性区块（比如搜索栏）不适合放入`<main>`，除非当前页面就是搜索页面。

### `<article>`

`<article>`标签表示页面里面一段完整的内容，即使页面的其他部分不存在，也具有独立使用的意义，通常用来表示一篇文章或者一个论坛帖子。它可以有自己的标题（`<h1>`到`<h6>`）。

```html
<article>
  <h2>文章标题</h2>
  <p>文章内容</p>
</article>
```

一个网页可以包含一个或多个`<article>`，比如包含多篇文章。

### `<aside>`

`<aside>`标签用来放置与网页或文章主要内容间接相关的部分。网页级别的`<aside>`，可以用来放置侧边栏，但不一定就在页面的侧边；文章级别的`<aside>`，可以用来放置补充信息、评论或注释。

下面是网页级别的`<aside>`的例子。

```html
<body>
  <main>主体内容</main>
  <aside>侧边栏</aside>
</body>
```

下面是文章评注的例子。

```html
<p>第一段</p>

<aside>
  <p>本段是文章的重点。</p>
</aside>
```

### `<section>`

`<section>`标签表示一个含有主题的独立部分，通常用在文档里面表示一个章节，比如`<article>`可以包含多个`<section>`。`<section>`总是多个一起使用，一个页面不能只有一个`<section>`。

```html
<article>
  <h1>文章标题</h1>
  <section>
    <h2>第一章</h2>
    <p>...</p>
  </section>
  <section>
    <h2>第二章</h2>
    <p>...</p>
  </section>
</article>
```

上面代码中，`<article>`包含了两个`<section>`，代表两章。

`<section>`很适合幻灯片展示的页面，每个`<section>`代表一个幻灯片。

一般来说，`<section>`都应该有标题，即包含`<h1>`~`<h6>`标签。多个`<section>`可以放置在同一个`<article>`里面，一个`<section>`里面也可能包含多个`<article>`，这取决于`<section>`和`<article>`在当前页面的含义。

### `<nav>`

`<nav>`标签用于放置页面或文档的导航信息。

```html
<nav>
  <ol>
    <li><a href="item-a">商品 A</a></li>
    <li><a href="item-b">商品 B</a></li>
    <li>商品 C</li>
  </ol>
</nav>
```

一般来说，`<nav>`往往放置在`<header>`里面，不适合放入`<footer>`。另外，一个页面可以有多个`<nav>`，比如一个用于站点导航，另一个用于文章导航。

`<nav>`里面通常是列表，但也可以放置其他标签。

### `<h1>` ~ `<h6>`

HTML 提供了6个标签，用来表示文章的标题。按照标题的等级，一共分成六级。

- `<h1>`：一级标题
- `<h2>`：二级标题
- `<h3>`：三级标题
- `<h4>`：四级标题
- `<h5>`：五级标题
- `<h6>`：六级标题

`<h1>`是最高级别的标题，`<h6>`是最低级别的标题。下一级标题都是上一级标题的子标题，比如，一个`<h1>`后面可以有多个`<h2>`，每个`<h2>`后面又可以有多个`<h3>`。

```html
<body>
  <h1>JavaScript 语言介绍</h1>
    <h2>概述</h2>
    <h2>基本概念</h2>
      <h3>网页</h3>
      <h3>链接</h3>
    <h2>主要用法</h2>
</body>
```

上面代码，通过章节标题，清晰地表明了文章的主体结构。具体的内容，就可以写在章节标题的下面。

标题不应该越级，比如`h1`下面直接写`h3`。虽然这样不会报错，但会导致文章失去清晰的章节结构。

默认情况下，浏览器会粗体显示标题。`h1`的字号比`h2`大，`h2`比`h3`大，以此类推。

### `<hgroup>`

如果主标题包含多级标题（比如带有副标题），那么可以使用`<hgroup>`标签，将多级标题放在其中。

```html
<hgroup>
  <h1>Heading 1</h1>
  <h2>Subheading 1</h2>
  <h2>Subheading 2</h2>
</hgroup>
```

注意，`<hgroup>`只能包含`<h1>`~`<h6>`，不能包含其他标签。

