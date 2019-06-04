# 图像

图片是互联网的重要组成部分，让网页变得丰富多彩。本章介绍如何在网页插入图片。

## `<img>`

`<img>`标签是一个行内元素，用于插入图片。它是单独使用的，没有闭合标签。

```html
<img src="foo.jpg">
```

上面代码在网页插入一张图片`foo.jpg`。`src`属性指定图片的网址，上例是相对 URL，表示图片与网页在同一个目录。

**（1）alt 属性**

图片下载需要时间，很可能网页已经展示在用户眼前，但是图片还没有下载完成。这时，网页不会显示图片，用户可能完全不会意识到，这里将会出现一张图片。另一种情况是，图片下载失败，浏览器会在图片位置显示一个图标，提示用户此处图片下载不成功。

为了让用户在图片不出现的情况下，了解图片和位置和内容，`<img>`标签提供了`alt`属性，用来设置图片的说明文字。图片不出现时，浏览器会显示这个文字说明。

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
