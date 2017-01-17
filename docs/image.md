# 图像

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
