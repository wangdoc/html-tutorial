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

## 通用属性

通用属性（global attributes）是那些所有元素都可以使用的属性。下面是一些常见的通用属性。

### id

`id`属性为网页元素提供文档范围的唯一标识符。比如，网页可能包含多个`<p>`标签，`id`属性可以指定每个`<p>`标签的唯一标识符。

```html
<p id="p1"></p>
<p id="p2"></p>
<p id="p3"></p>
```

上面代码中，三个`<p>`标签具有不同的`id`属性，因此可以加以区分。

`id`属性的值必须是全局唯一的，同一个页面不能有两个相同的`id`属性。

`id`属性的值还可以在头部加上`#`，然后放到 URL 的网页文件名后面，比如`https://foo.com/index.html#bar`。用户访问这个 URL 的时候，浏览器就会自动将页面滚动到`bar`的位置，方便用户第一眼就看到这部分内容。

### class

`class`属性用来对网页元素进行分类。如果不同元素的`class`属性值相同，就表示它们是一类的。

```html
<p class="para"></p>
<p></p>
<p class="para"></p>
```

上面代码中，第一个`<p>`和第三个`<p>`是一类，因为它们的`class`属性相同。

### title

`title`属性用来为元素添加附加说明。大多数浏览器中，鼠标悬浮在元素上面时，会将`title`属性值作为提示，显示出来。

### style

`style`属性用来指定元素的样式。

### lang，dir

`lang`属性指定元素使用的语言。

```html
<p lang="en">hello</p>
<p lang="zh">你好</p>
```

上面代码中，第一个`<p>`的`lang`属性，表示使用英语，第二个`<p>`的`lang`属性，表示使用中文。

`dir`属性表示文字的阅读方向，默认值是`ltr`，表示从左到右。另一个可能的值是`rtl`，表示从右到左，阿拉伯语、波斯语、希伯来语都属于这一类。

### 事件处理属性

除了上面这些属性，通用属性还包括事件处理属性（event handler），它们用来响应用户的动作。这些属性的值都是 JavaScript 代码，就放在 JavaScript 教程介绍了，这里只列出这些属性的名单。

> onabort, onautocomplete, onautocompleteerror, onblur, oncancel, oncanplay, oncanplaythrough, onchange, onclick, onclose, oncontextmenu, oncuechange, ondblclick, ondrag, ondragend, ondragenter, ondragexit, ondragleave, ondragover, ondragstart, ondrop, ondurationchange, onemptied, onended, onerror, onfocus, oninput, oninvalid, onkeydown, onkeypress, onkeyup, onload, onloadeddata, onloadedmetadata, onloadstart, onmousedown, onmouseenter, onmouseleave, onmousemove, onmouseout, onmouseover, onmouseup, onmousewheel, onpause, onplay, onplaying, onprogress, onratechange, onreset, onresize, onscroll, onseeked, onseeking, onselect, onshow, onsort, onstalled, onsubmit, onsuspend, ontimeupdate, ontoggle, onvolumechange, onwaiting
