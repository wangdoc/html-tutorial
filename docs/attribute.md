# 网页元素的属性

## 简介

HTML 允许通过网页元素的属性（attribute），定制元素的行为。写法上，表现为标签内部的“键值对”。

```html
<html lang="en">
```

上面代码中，`<html>`标签内部的键值对`lang="en"`，就称为`html`元素的属性。属性名为`lang`，属性值为`en`。

属性名与标签名一样，不区分大小写，`lang`和`LANG`是同一个属性。

属性名与属性值之间，通过等号`=`连接。属性值可以放在单引号或双引号之中，建议统一使用双引号。某些属性值可以不使用引号，但是建议避免这种做法。

有些属性是布尔属性，即属性值是一个布尔值，只有“打开”和“关闭”两种情况。这时属性值可以省略，只要添加了属性名，就表示打开该属性。

```html
<input type="text" required>
```

上面代码中，`required`就是`<input>`标签的布尔属性。如果没有这个属性，就表示关闭，否则就是打开。

## 全局属性

全局属性（global attributes）是那些所有元素都可以使用的属性。也就是说，你可以把下面的属性，加在任意一个元素上面，不过对某些元素可能不产生意义。下面是一些常见的全局属性。

### id

`id`属性为网页元素提供文档范围的唯一标识符。比如，网页可能包含多个`<p>`标签，`id`属性可以指定每个`<p>`标签的唯一标识符。

```html
<p id="p1"></p>
<p id="p2"></p>
<p id="p3"></p>
```

上面代码中，三个`<p>`标签具有不同的`id`属性，因此可以加以区分。

`id`属性的值必须是全局唯一的，同一个页面不能有两个相同的`id`属性。另外，`id`属性的值不得包含空格。

`id`属性的值还可以在头部加上`#`，然后放到 URL 的网页文件名后面，表示指定指定网页内部的位置，比如`https://foo.com/index.html#bar`。用户访问这个 URL 的时候，浏览器就会自动将页面滚动到`bar`的位置，让用户第一眼就看到这部分内容。

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

### style

`style`属性用来指定当前元素的 CSS 样式。

```html
<p style="color: red;">hello</p>
```

上面代码指定文字颜色为红色。

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

## contenteditable

HTML 网页的内容默认是不能修改，`contenteditable`属性允许用户修改内容。它有两个可能的值。

- `true`或空字符串：内容可以编辑
- `false`：不可以编辑

```html
<p contenteditable="true">
鼠标点击，本句内容可修改。
</p>
```

上面代码中，鼠标单击句子，就可以进入修改状态，用户可以改变句子的内容。当然，除非提交到服务器，否则刷新页面还是显示原来的内容。

该属性是枚举属性，不是布尔属性，所以使用的时候，应该带上属性值。

## spellcheck

浏览器自带拼写检查功能，编辑内容时，拼错的单词下面会显示红色的波浪线。`spellcheck`属性就表示，是否打开拼写检查。

它有两个可能的值。

- `true`：打开拼写检查
- `false`：关闭拼写检查

```html
<p contenteditable="true" spellcheck="true">
英语单词 separate 容易写错成 seperate。
</p>
```

上面代码中，`seperate`下面会有提示，表示拼错了。

注意，由于该属性只在编辑时生效，所以这个例子必须加上`contenteditabl`属性，表示本段内容可编辑。鼠标单击就可以进入编辑状态，这时才会看到拼写提示。正常状态下，拼写提示是不显示的。对于那些不可编辑的元素，该属性无效。

这个属性看上去像布尔属性，但是其实是枚举属性，所以它的值不能省略。如果没有指定这个属性，由浏览器自行决定是否打开拼写检查。

### 事件处理属性

除了上面这些属性，通用属性还包括事件处理属性（event handler），它们用来响应用户的动作。这些属性的值都是 JavaScript 代码，就放在 JavaScript 教程介绍了，这里只列出这些属性的名单。

> onabort, onautocomplete, onautocompleteerror, onblur, oncancel, oncanplay, oncanplaythrough, onchange, onclick, onclose, oncontextmenu, oncuechange, ondblclick, ondrag, ondragend, ondragenter, ondragexit, ondragleave, ondragover, ondragstart, ondrop, ondurationchange, onemptied, onended, onerror, onfocus, oninput, oninvalid, onkeydown, onkeypress, onkeyup, onload, onloadeddata, onloadedmetadata, onloadstart, onmousedown, onmouseenter, onmouseleave, onmousemove, onmouseout, onmouseover, onmouseup, onmousewheel, onpause, onplay, onplaying, onprogress, onratechange, onreset, onresize, onscroll, onseeked, onseeking, onselect, onshow, onsort, onstalled, onsubmit, onsuspend, ontimeupdate, ontoggle, onvolumechange, onwaiting
