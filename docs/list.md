# 列表标签

## `<dl>`

`<dl>`标签是一个块级元素，表示一组术语的列表（description list）。术语名（description term）由`<dt>`标签定义，术语解释（description detail）由`<dd>`标签定义。`<dl>`常用来定义词汇表。

```html
<dl>
  <dt>CPU</dt>
  <dd>中央处理器</dd>

  <dt>Memory</dt>
  <dd>内存</dd>

  <dt>Hard Disk</dt>
  <dd>硬盘</dd>
</dl>
```

`<dt>`和`<dd>`都是块级元素，`<dd>`默认会在`<dt>`下方缩进显示。上面代码的默认渲染结果如下。

```html
CPU
  中央处理器

Memory
  内存

Hard Disk
  硬盘
```

多个术语对应一个解释，或者多个术语对应一个解释，都是合法的。

```html
<dl>
  <dt>Foo</dt>
  <dt>Bar</dt>
  <dd>baz</dd>

  <dt>Foo</dt>
  <dd>bar</dd>
  <dd>baz</dd>
</dl>
```

