# 图像

图片是互联网的重要组成部分，让网页变得丰富多彩。本章介绍如何在网页插入图片。

## `<img>`

`<img>`标签用于插入图片。它是单独使用的，没有闭合标签。

```html
<img src="foo.jpg">
```

上面代码在网页插入一张图片`foo.jpg`。`src`属性指定图片的网址，上例是相对 URL，表示图片与网页在同一个目录。

`<img>`默认是一个行内元素，与前后的文字处在同一行。

```html
<p>Hello<img src="foo.jpg">World</p>
```

上面代码的渲染结果是，文字和图片在同一行显示。

图像默认以原始大小显示。如果图片很大，又与文字处在同一行，那么图片将把当前行的行高撑高，并且图片的底边与文字的底边在同一条水平线上。

`<img>`可以放在`<a>`标签内部，使得图片变成一个可以点击的链接。

```html
<a href="example.html">
  <img src="foo.jpg">
</a>
```

上面代码中，图片可以像链接那样点击，点击后会产生跳转。

**（1）alt 属性**

`alt`属性用来设定图片的文字说明。图片不显示时（比如下载失败，或用户关闭图片加载），图片的位置上会显示该文本。

```html
<img src="foo.jpg" alt="示例图片">
```

上面代码中，`alt`是图片的说明。图片下载进行中或下载失败时，浏览器会在图片位置，显示文字“示例图片”。

**（2）width 属性，height 属性**

图片默认以原始大小插入网页，`width`属性和`height`属性可以指定图片显示时的宽度和高度，单位都是像素或百分比。

```html
<img src="foo.jpg" width="400" height="300">
```

上面代码中，`width`属性指定图片显示的宽度为400像素，`height`属性指定显示高度为300像素。

注意，一旦设置了这两个属性，浏览器会在网页中预先留出这个大小的空间，不管图片有没有加载成功。不过，由于图片的显示大小可以用 CSS 设置，所以不建议使用这两个属性。

特殊情况是，`width`属性和`height`属性只设置了一个，另一个没有设置。这时，浏览器会根据图片的原始大小，自动设置对应比例的图片宽度或高度。举例来说，图片大小是 800像素 x 800像素，`width`属性设置成200，那么浏览器会自动将`height`设成200。

**（3）srcset，sizes**

`srcset`属性设定同一张图片的多个版本，用于不同环境的浏览器使用。比如，桌面浏览器下载桌面版本的图片，手机浏览器下载手机版本的图片，这样有利于提高网页的性能，节省带宽。

`srcset`属性的值是多个图片网址，每个之间使用逗号分隔。

```html
<img srcset="foo-320w.jpg,
             foo-480w.jpg 1.5x,
             foo-640w.jpg 2x"
     src="foo-640w.jpg">
```

上面代码中，`srcset`属性设置三张图片的网址，它们之间使用逗号分隔。

每个图片网址后面还带有一个说明符，两者之间是一个空格。说明符有两种格式，一种是像素密度+字母`x`，比如`1x`、`2x`，就像上例。如果省略了说明符，默认为`1x`。另一种是图片文件的实际宽度（单位像素）+ 字母`w`。两种说明符只能选择一种格式，不能两者同时设置。

第一种格式的情况下，浏览器会根据当前设备的像素密度，选择对应的图片。上例中，如果当前设备是`2x`的高分辨率屏幕，那么就会加载`foo-640w.jpg`这个文件。如果实际的像素密度不在`srcset`属性指定的范围内，那么将加载`src`属性指定的默认图片文件。

除了高分辨率屏幕，更多的情况是设备的屏幕大小不同，这时就需要第二张格式，并且需要配合`sizes`属性一起使用。

```html
<img srcset="foo-320w.jpg 320w,
             foo-480w.jpg 480w,
             foo-800w.jpg 800w"
     sizes="(max-width: 320px) 280px,
            (max-width: 480px) 440px,
            800px"
     src="foo-800w.jpg">
```

第二种格式的情况下，浏览器先查看`sizes`属性。`sizes`属性也由多个逗号分隔的字符串组成，除了最后一部分，每一个字符串的前面部分都是“媒体查询条件+空格+图片宽度”的形式，最后一部分则只有图片宽度，匹配所有其他情况。

如果当前设备的屏幕宽度在320像素到480像素之间，那么符合`sizes`属性的第二个条件，浏览器由此得知图片宽度应为440像素。然后，浏览器检查`srcset`属性，发现最符合440像素的图片，是`480w`那一档的`foo-800w.jpg`。如果没有符合条件的图片，那么将加载`src`属性指定的默认图片。

注意，如果没有`srcset`属性，`sizes`属性无效。

**（4）referrerpolicy**

`<img>`发起的 HTTP 请求，默认会带有`Referer`的头信息。`referrerpolicy`属性对这个行为进行设置。

**（5）crossorigin**

有些外部资源的下载，对方服务器可能要求跨域认证。`crossorigin`属性告诉浏览器，是否采用跨域的形式下载图片，默认是不采用。下面是简单解释，详细解释请参考相关的 HTTP 教程。

只要打开了这个属性，HTTP 请求的头信息里面，就会加入`origin`字段，给出请求发出的域名，不打开这个属性就不加。

该属性可以设为两个值。

- `anonymous`：跨域请求不带有用户凭证（通常是 Cookie）。
- `use-credentials`：跨域请求带有用户凭证。

下面是一个例子。

```html
<img src="foo.jpg" crossorigin="anonymous">
```

`crossorigin`属性如果省略值的部分，则等同于`anonymous`。

```html
<img src="foo.jpg" crossorigin>
```

## `<figure>`，`<figcaption>`

`<figure>`标签可以理解是一个图像区块，将图像和相关信息封装在一起。`<figcaption>`是它的可选的子元素，表示图像的标题。

```html
<figure>
  <img src="https://example.com/foo.jpg">
  <figcaption>示例图片</figcaption>
</figure>
```

除了图像，`<figure>`还可以封装引言、代码、诗歌等等。它等于是一个将主体内容与附加信息，封装在一起的语义容器。

## srcset 属性

`<img>`标签的`srcset`属性，允许列出多个可用于替代的图片数据源，浏览器可以针对不同的用户设备，选择显示合适的图片。比如，在低速网络和小屏幕手机的情况下，应该为用户提供低像素的图片。

`srcset`属性接受一个用逗号分隔的 URL 列表，每个 URL 后面带有`x`字符串，表示适用的图片像素比。

```html
<img src="images/low-res.jpg" srcset="
  images/low-res.jpg 1x,
  images/high-res.jpg 2x,
  images/ultra-high-res.jpg 3x"
>
```

上面代码中，如果用户设备的图片像素比是`1`，浏览器显示`low-res.jpg`；如果是`2`，浏览器显示`high-res.jpg`；如果是`3`，浏览器显示`ultra-high-res.jpg`。

除了`x`字符串，还可以使用`w`字符串，表示图片的宽度（单位为像素）。

```javascript
<img src="images/low-res.jpg" srcset="
  images/low-res.jpg 500w,
  images/high-res.jpg 1000w,
  images/ultra-high-res.jpg 2000w"
>
```

上面代码中，`low-res.jpg`的宽度是500像素，`high-res.jpg`是1000像素，`ultra-high-res.jpg`是2000像素。现在有一个`320px`宽度和`1x`设备像素比（即非 retina）的设备，浏览器会进行下面的计算。

```
500 / 320 = 1.5625
1000 / 320 = 3.125
2000 / 320 = 6.25
```

上面代码中，`1.5626`最接近设备像素比`1x`，所以展示`low-res.jpg`。如果是`2x`设备像素比，`3.125`最接近这个值，所以显示`high-res.jpg`。

## sizes 属性

`sizes`属性用于根据设备的不同，显示不同宽度的图像。

```html
<img src="images/low-res.jpg" sizes="(max-width: 40em) 100vw, 50vw">
```

上面代码中，视口宽度小于`40em`时，图片显示的宽度为`100vw`；否则，显示的宽度为`50vw`。

## picture 标签

`srcset`属性主要用于，不同宽度的设备显示同一张图片的不同版本。如果想根据不同的设备，使用不同的图片，就应该使用`<picture>`标签。

`<picture>`指定多个不同`<source>`元素，来为不同尺寸的屏幕定义不同的图片。

```html
<picture>
  <source media="(max-width: 20em)" srcset="
    images/small/low-res.jpg 1x,
    images/small/high-res.jpg 2x,
    images/small/ultra-high-res.jpg 3x
  ">
  <source media="(max-width: 40em)" srcset="
    images/large/low-res.jpg 1x,
    images/large/high-res.jpg 2x,
    images/large/ultra-high-res.jpg 3x
  ">

  <img src="images/large/low-res.jpg">
</picture>
```
