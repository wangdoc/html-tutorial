# 网页的语义结构

## 含义

HTML 标签的一个重要作用，就是声明网页元素的性质，使得用户只看标签，就能了解这个元素的意义，阅读 HTML 源码就能了解网页的大致结构。这被称为 HTML 的语义（semantic）原则。

下面就是一个典型的语义结构的网页。

```html
<body>
  <header>页头</header>
  <main>
    <article>
      <h1>文章标题</h1>
      <p>文章内容</p>
    </article>
  </main>
  <footer>页尾</footer>
</body>
```

只看上面的代码，就可以知道，页面分成页头、主体、页尾三个部分。

编写 HTML 网页，第一步就是写出语义结构的网页骨架。

## 常用标签

### `<header>`

`<header>`标签可以用在多个场景，分别表示网页、文章、章节的头部。如果是网页的头部，就称为“页眉”，网站导航和搜索栏通常会放在`<header>`里面。

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

如果`<header>`用在文章的头部，可以把文章标题、作者等信息放进去。

```html
<article>
  <header>
    <h2>文章标题</h2>
    <p>张三，发表于2010年1月1日</p>
  </header>
</article>
```

由于`<header>`可以用在多种场景，所以一个页面可能包含多个`<header>`，但是一个场景只能包含一个。另外，`<header>`里面不能包含另一个`<header>`或`<footer>`。

### `<footer>`

`<footer>`标签表示整张网页或文章或章节的尾部。如果用于整张网页，就称为“页尾”，通常包含版权信息或者其他相关信息。

```html
<body>
  <footer>
    <p>© 2018 xxx 公司</p>
  </footer>
</body>
```

`<footer>`也可以放在文章里面。

```html
<article>
  <header>
    <h1>文章标题</h1>
  </header>
  <footer>
    <p>© 禁止转贴</p>
  </footer>
</body>
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

`<article>`标签表示页面里面一段完整的内容，可以用来表示一篇文章或者一个论坛帖子。

```html
<article>
  <h2>文章标题</h2>
  <p>文章内容</p>
</article>
```

一个网页可以包含多个`<article>`，比如包含多篇文章。另外，`<article>`可以嵌套，比如文章里面的读者评论，可以是另外一个`<article>`。

### `<aside>`

`<aside>`标签用来放置与网页或文档主要内容间接相关的部分。网页级别，可以用来放置侧边栏；文档级别，可以用来放置评论或注释。

下面是侧边栏的例子。

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

`<section>`标签表示一个含有主题的独立部分，通常用在文档里面表示一个章节。一个`<article>`可以包含多个`<section>`。

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

上面代码中，`<article>`包含了两个`<section>`，代表两章。由此可以想到，`<section>`很适合幻灯片展示的页面，每个`<section>`代表一个幻灯片。

一般来说，`<section>`都应该有标题，即包含`<h1>`~`<h6>`标签。另外，如果多个`<section>`联合在一起是有意义的，那么它们应该放置在同一个`<article>`里面。

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

一般来说，`<nav>`都是放置在`<header>`里面，`<footer>`里面的链接不适合放入`<nav>`。另外，一个页面可以有多个`<nav>`，比如一个用于站点导航，另一个用于文章导航。

### Label

`Label`用于为指定的表单元素，提供解释性文本。

它有两种用法。

```html
<!-- 用法一 -->
<label>
  <input type="checkbox" name="quokka">
  Yes, I want to buy a quokka!
</label>

<!-- 用法二 -->
<input type="checkbox" id="yayforwallaby"
       name="wallaby">
<label for="yayforwallaby">
  Yes, I want to buy a wallaby!
</label>
```

注意，在用法二之中，表单元素必须有`id`属性，`label`元素的`for`属性匹配的是`id`属性，而不是`name`属性。`name`属性用于将这个表单元素的值发送到服务器。

另一点需要注意的是，在JavaScript之中，`for`属性无法以`element.for`的形式获取，因为`for`是一个JavaScript保留字，必须改用`htmlfor`表示。

```javascript
var labels = document.querySelectorAll('label');
for (var i=0; i<labels.length; i++) {
  if (labels[i].htmlFor) {
    if (!document.getElementById(labels[i].htmlFor)) {
      labels[i].style.background = 'firebrick';
    }
  }
}
```

### Main

Main标签表示文档的主要部分。

### Meter

Meter标签表示某个范围内的度量值。

```html
<meter>1 of 10</meter>
<meter>2 of 7</meter>
```

它有6个属性。

- value
- min
- max
- high
- low
- optimum

```html
Your batting average is <meter value=".340" min="0" max="1.000" low=".215" high=".367" optimum="1.000">.340</meter>
```

### Nav

Nav标签表示文档的导航部分，通常可以放在Header部分之中。

### Progress

Progress标签表示进度。

```html
Your download is <progress>55%</progress> complete
```

它有三个属性。

- value
- min
- max

### Section

section标签代表文档的一个部分。

```html
<section>
  <h1>Bob Dylan Albums</h1>
  <p>Some text</p>

  <section>
    <h2>Blood on the Tracks</h2>
    <p>Some text</p>
  </section>

  <section>
    <h2>Highway 61 Revisited</h2>
    <p>Some text</p>
  </section>

  <p>Some text</p>
</section>
```

### Time

Time标签用来表示时间。

```html
<time>2011-07-14</time>
<time datetime="14:00">2pm</time>
<time datetime="2011-07-14">July 14th, 2011</time>
<time datetime="2011-07-14T14:00">2pm on July 14th</time>
```

### Video

`video`元素用于插入视频元素。

```html
<video
  src="#defer-loading"
  poster="nice-default.jpg
  autoplay
/>
```

下面是将视频全屏插入网页，作为背景 。

```css
video.fullscreen {
  position: fixed;
  top: 50%;
  left: 50%;
  min-width: 100%;
  min-height: 100%;
  width: auto;
  height: auto;
  z-index: -100;
  transform: translate(-50%, -50%);
}
```

参考链接

- [Should I use a video as a background?](https://css-tricks.com/should-i-use-a-video-as-a-background/)

