# picture

`<picture>`用来部署响应式图片，根据不同的客户端，加载不同的图片。

`<picture>`元素内部包含若干个`<source>`元素和一个`<img>`元素。`<source>`元素具有`srcset`属性和`media`属性，其中`media`属性的值是一个 Media Query 表达式。

```html
<picture>
  <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg">
  <source media="(min-width: 800px)" srcset="elva-800w.jpg">
  <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
</picture>
```

如果客户端满足某个`media`属性，则会加载该`<source>`元素指定的图片。如果所有`<source>`元素都不满足，则会加载`<img>`元素指定的图片。

注意，客户端发现第一个满足条件的`<source>`元素，就不再会检查后面的元素。这也意味着`<source>`元素的位置一定要在`<img>`元素的前面。

`<source>`元素还具有`type`属性，用来指定当前加载图片的 MIME 类型。如果客户端支持该类型，就会加载指定的图片。

```html
<picture>
  <source type="image/svg+xml" srcset="pyramid.svg">
  <source type="image/webp" srcset="pyramid.webp"> 
  <img src="pyramid.png" alt="regular pyramid built from four equilateral triangles">
</picture>
```

