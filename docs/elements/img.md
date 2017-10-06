# img

`<img>`元素用来插入图片。

`alt`属性用来设定图片的文字说明，图片没有显示时（比如 URL 错误或没有下载成功），图片的位置上会显示该文本。

```html
<img src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
```

`srcset`属性是一个逗号分隔的序列，指定多个图片网址。

`sizes`属性是一个逗号分隔的序列，用来指定 Media Query 的条件，与`srcset`属性一一对应。客户端只要符合某个 Media Query，就会加载`srcset`里面对应的图片 URL。

```html
<img srcset="elva-fairy-320w.jpg 320w,
             elva-fairy-480w.jpg 480w,
             elva-fairy-800w.jpg 800w"
     sizes="(max-width: 320px) 280px,
            (max-width: 480px) 440px,
            800px"
     src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
```

上面代码中，`srcset`属性里面每个 URL 后面，跟着图片的真实宽度，使用`w`作为后缀。`sizes`属性里面每个 Media Query 后面，跟着图片的显示宽度。

浏览器遇到这个`<img>`元素，会进行下面的步骤。

1. 根据当前设备的宽度，决定`sizes`属性里面哪一个 Media Query 首先为真。
1. 检查这个 Media Query 里面跟的显示宽度，根据`srcset`属性里面哪一个图片宽度，决定最接近这个显示宽度的图片。
1. 加载该图片。

举例来说，设备的视口宽度是480px，那么将满足`(max-width: 480px)`这个条件，因此显示宽度是440px。最接近的图片宽度是480px，所以会加载`elva-fairy-480w.jpg`这张图片。

`sizes`属性里面的显示宽度，不一定设为像素，其他宽度单位也是可以的。

```html
<img src="small.jpg"
     srcset="large.jpg 1024w, medium.jpg 640w, small.jpg 320w"
     sizes="(min-width: 36em) 33.3vw, 100vw"
     alt="A swirling nebula">
```

另一种情况是`srcset`属性指定不同的像素密度，所对应要加载的图片。

```html
<img
  srcset="elva-fairy-320w.jpg,
    elva-fairy-480w.jpg 1.5x,
    elva-fairy-640w.jpg 2x"
  src="elva-fairy-640w.jpg"
  alt="Elva dressed as a fairy"
>
```

上面代码中，标准密度的屏幕会加载`elva-fairy-320w.jpg`，1.5倍密度的屏幕会加载`elva-fairy-480w.jpg`，2倍密度的屏幕会加载`elva-fairy-640w.jpg`。

## 参考链接

- [Responsive images](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images), by Mozilla
