# 网页元素的属性

## 简介

网页元素的属性（attribute）可以定制元素的行为，不同的属性会导致元素有不同的行为。元素属性的写法是 HTML 标签内部的“键值对”。

```html
<html lang="en">
```

上面代码中，`<html>`标签内部的键值对`lang="en"`，就称为`html`元素的属性。属性名为`lang`，属性值为`en`。

属性名与标签名一样，不区分大小写，`lang`和`LANG`是同一个属性。

属性名与属性值之间，通过等号`=`连接。属性值可以放在单引号或双引号之中，建议统一使用双引号。某些属性值可以不使用引号，但是建议不要这样写。

有些属性是布尔属性，即属性值是一个布尔值，只有“打开”和“关闭”两种情况。这时属性值可以省略，只要添加了属性名，就表示打开该属性。

```html
<input type="text" required>
```

上面代码中，`required`就是`<input>`标签的布尔属性。如果加上这个属性，就表示打开，没有就是关闭。

## 全局属性

全局属性（global attributes）是所有元素都可以使用的属性。也就是说，你可以把下面的属性，加在任意一个网页元素上面，不过有些属性对某些元素可能不产生意义。

下面是一些常见的全局属性。

### id

`id`属性是元素在网页内的唯一标识符。比如，网页可能包含多个`<p>`标签，`id`属性可以指定每个`<p>`标签的唯一标识符。

```html
<p id="p1"></p>
<p id="p2"></p>
<p id="p3"></p>
```

上面代码中，三个`<p>`标签具有不同的`id`属性，因此可以区分。

`id`属性的值必须是全局唯一的，同一个页面不能有两个相同的`id`属性。另外，`id`属性的值不得包含空格。

`id`属性的值还可以在最前面加上`#`，放到 URL 中作为锚点，定位到该元素在网页内部的位置。比如，用户访问网址`https://foo.com/index.html#bar`的时候，浏览器会自动将页面滚动到`bar`的位置，让用户第一眼就看到这部分内容。

### class

`class`属性用来对网页元素进行分类。如果不同元素的`class`属性值相同，就表示它们是一类的。

```html
<p class="para"></p>
<p></p>
<p class="para"></p>
```

上面代码中，第一个`<p>`和第三个`<p>`是一类，因为它们的`class`属性相同。

元素可以同时具有多个 class，它们之间使用空格分隔。

```html
<p class="p1 p2 p3"></p>
```

上面的`p`元素同时具有`p1`、`p2`、`p3`三个 class。

### title

`title`属性用来为元素添加附加说明。大多数浏览器中，鼠标悬浮在元素上面时，会将`title`属性值作为浮动提示，显示出来。

```html
<div title="版权说明">
  <p>本站内容使用创意共享许可证，可以自由使用。</p>
</div>
```

上面代码中，`title`属性解释了这一块内容的目的。鼠标悬停在上面时，浏览器会显示一个浮动提示。一旦鼠标移开，提示就会消失。

### tabindex

网页通常使用鼠标操作，但是某些情况下，用户可能希望使用键盘，或者只有键盘可以用。因此，浏览器允许使用 Tab 键，遍历网页元素。也就是说，只要不停按下 Tab 键，网页的焦点就会从一个元素转移到另一个元素，选定焦点元素以后，就可以进行下一步操作，比如按下回车键访问某个链接，或者直接在某个输入框输入文字。

这里就有一个问题，按下 Tab 键的时候，浏览器怎么知道跳到哪一个元素。HTML 提供了`tabindex`属性，解决这个问题。它的名字的含义，就是 Tab 的顺序（index）。

`tabindex`属性的值是一个整数，表示用户按下 Tab 键的时候，网页焦点转移的顺序。不同的属性值有不同的含义。

- 负整数：该元素可以获得焦点（比如使用 JavaScript 的`focus()`方法），但不参与 Tab 键对网页元素的遍历。这个值通常是`-1`。
- `0`：该元素参与 Tab 键的遍历，顺序由浏览器指定，通常是按照其在网页里面出现的位置。
- 正整数：网页元素按照从小到大的顺序（1、2、3、……），参与 Tab 键的遍历。如果多个元素的`tabindex`属性相同，则按照在网页源码里面出现的顺序遍历。

```html
<p tabindex="0">这段文字可以获得焦点。</p>
```

上面代码中，`<p>`标签的`tabindex`为`0`，意味着该元素可以获得焦点，并且也可以被 Tab 键遍历，顺序由其在源码里面的位置决定。

一般来说，`tabindex`属性最好都设成`0`，按照自然顺序进行遍历，这样比较符合用户的预期，除非网页有特殊布局。如果网页所有元素都没有设置`tabindex`，那么只有那些默认可以遍历的元素（比如链接、输入框等）才能参与 Tab 键的遍历，顺序由其在源码的位置决定。因此实际上，只有那些无法获得焦点的元素（比如`<span>`、`<div>`）需要参与遍历，才有必要设置`tabindex`属性。

### accesskey

`accesskey`属性指定网页元素获得焦点的快捷键，该属性的值必须是单个的可打印字符。只要按下快捷键，该元素就会得到焦点。

```html
<button accesskey="s">提交</button>
```

上面代码中，`<button>`的快捷键是`s`，按下快捷键，该元素就得到了焦点。

`accesskey`属性的字符键，必须配合功能键，一起按下才会生效。也就是说，快捷键是“功能键 + 字符键”的组合。不同的浏览器与不同的操作系统，功能键都不一样。比如，Chrome 浏览器在 Windows 系统和 Linux 系统的快捷键是`Alt + 字符键`，在 Mac 系统的快捷键是`Ctrl + Alt + 字符键`。

注意，`accesskey`如果跟操作系统或浏览器级别的快捷键有冲突，这时不会生效。

### style

`style`属性用来指定当前元素的 CSS 样式。具体的设置，请看 CSS 教程。

```html
<p style="color: red;">hello</p>
```

上面代码指定文字颜色为红色。

### hidden

`hidden`是一个布尔属性，表示当前的网页元素不再跟页面相关，因此浏览器不会渲染这个元素，所以就不会在网页中看到它。

```html
<p hidden>本句不会显示在页面上。</p>
```

上面代码中，这个`p`元素不会出现在网页上。

注意，CSS 的可见性设置，高于`hidden`属性。如果 CSS 设为该元素可见，`hidden`属性将无效。

### lang，dir

`lang`属性指定网页元素使用的语言。

```html
<p lang="en">hello</p>
<p lang="zh">你好</p>
```

上面代码中，第一个`<p>`的`lang`属性，表示使用英语，第二个`<p>`的`lang`属性，表示使用中文。

`lang`属性的值，必须符合 [BCP47](https://www.ietf.org/rfc/bcp/bcp47.txt) 的标准。下面是一些常见的语言代码。

- zh：中文
- zh-Hans：简体中文
- zh-Hant：繁体中文
- en：英语
- en-US：美国英语
- en-GB：英国英语
- es：西班牙语
- fr：法语

`dir`属性表示文字的阅读方向，有三个可能的值。

- `ltr`：从左到右阅读，比如英语。
- `rtl`：从右到左阅读，阿拉伯语、波斯语、希伯来语都属于这一类。
- `auto`：浏览器根据内容的解析结果，自行决定。

### contenteditable

HTML 网页的内容默认是用户不能编辑，`contenteditable`属性允许用户修改内容。它有两个可能的值。

- `true`或空字符串：内容可以编辑
- `false`：不可以编辑

```html
<p contenteditable="true">
鼠标点击，本句内容可修改。
</p>
```

上面代码中，鼠标单击句子，就可以进入编辑状态，用户可以改变句子的内容。当然，除非提交到服务器，否则刷新页面还是显示原来的内容。

该属性是枚举属性，不是布尔属性，规范的写法是最好带上属性值。

### spellcheck

浏览器一般会自带拼写检查功能，编辑内容时，拼错的单词下面会显示红色的波浪线。`spellcheck`属性就表示，是否打开拼写检查。

它有两个可能的值。

- `true`：打开拼写检查
- `false`：关闭拼写检查

```html
<p contenteditable="true" spellcheck="true">
英语单词 separate 容易写错成 seperate。
</p>
```

上面代码中，`seperate`下面会有提示，表示拼错了。

注意，由于该属性只在编辑时生效，所以这个例子必须加上`contenteditable`属性，表示本段内容可编辑。鼠标单击就可以进入编辑状态，这时才会看到拼写提示。不可编辑的状态下，拼写错误是不提示显示的。对于那些不可编辑的元素，该属性无效。

这个属性看上去像布尔属性，但是其实是枚举属性，所以最好不要省略它的值。如果没有指定这个属性，浏览器将自行决定是否打开拼写检查。

### `data-`属性

`data-`属性用于放置自定义数据。如果没有其他属性或元素合适放置数据，就可以放在`data-`属性。

```html
<a href="#" class="tooltip" data-tip="this is the tip!">链接</a>
```

上面代码中，`data-tip`用于放置链接的提示文字。

由于`data-`属性只能通过 CSS 或 JavaScript 利用，所以这里不做详细介绍了。下面是 CSS 的例子。

```css
/* HTML 代码如下
<div data-role="mobile">
Mobile only content
</div>
*/
div[data-role="mobile"] {
  display:none;
}

/* HTML 代码如下
<div class="test" data-content="This is the div content">test</div>​
*/
.test {
  display: inline-block;
}
.test:after {
  content: attr(data-content);
}
```

### 事件处理属性

除了上面这些属性，全局属性还包括事件处理属性（event handler），用来响应用户的动作。这些属性的值都是 JavaScript 代码，请参考 JavaScript 教程，这里只列出这些属性的名单。

> onabort, onautocomplete, onautocompleteerror, onblur, oncancel, oncanplay, oncanplaythrough, onchange, onclick, onclose, oncontextmenu, oncuechange, ondblclick, ondrag, ondragend, ondragenter, ondragexit, ondragleave, ondragover, ondragstart, ondrop, ondurationchange, onemptied, onended, onerror, onfocus, oninput, oninvalid, onkeydown, onkeypress, onkeyup, onload, onloadeddata, onloadedmetadata, onloadstart, onmousedown, onmouseenter, onmouseleave, onmousemove, onmouseout, onmouseover, onmouseup, onmousewheel, onpause, onplay, onplaying, onprogress, onratechange, onreset, onresize, onscroll, onseeked, onseeking, onselect, onshow, onsort, onstalled, onsubmit, onsuspend, ontimeupdate, ontoggle, onvolumechange, onwaiting

