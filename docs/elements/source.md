# source

`<source>`元素用于`<picture>`、`<audio>`、`<video>`元素之中，提供多个媒体资源，供客户端选择加载其中的一个。

`<source>`元素如果用于`<picture>`元素之中，需要有`srcset`属性；如果用于`<audio>`、`<video>`元素之中需要有`src`属性。

```html
<picture>
  <source srcset="mdn-logo-wide.png" media="(min-width: 600px)">
  <img src="mdn-logo-narrow.png" alt="MDN">
</picture>

<video controls>
  <source src="foo.webm" type="video/webm">
  <source src="foo.ogg" type="video/ogg"> 
  <source src="foo.mov" type="video/quicktime">
  I'm sorry; your browser doesn't support HTML5 video.
</video>
```

上面代码中，`<source>`元素的`media`属性用来指定客户端的 Media Query，`type`属性用来指定加载的多媒体资源的 MIME 类型。客户端使用它们，决定要加载哪一个`<source>`元素。

`<source>`元素的`sizes`属性和`srcset`属性的使用规则，参看`<img>`元素的说明。

```html
<picture>
  <source media="(min-width: 70em)"
          sizes="40vw"
          srcset="nebula-artsy-wide-2800.jpg 2800w,
                  nebula-artsy-wide-2240.jpg 2240w,
                  nebula-artsy-wide-1400.jpg 1400w,
                  nebula-artsy-wide-1120.jpg 1120w">
  <source media="(min-width: 35em)"
          sizes="36vw"
          srcset="nebula-artsy-square-1120.jpg 1120w,
                  nebula-artsy-square-900.jpg 900w,
                  nebula-artsy-square-560.jpg 560w,
                  nebula-artsy-square-450.jpg 450w">
  <img src="nebula-artsy-tight.jpg" alt="An artsy cat">
</picture>
```
