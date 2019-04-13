# <details>，<summary>

`<details>`标签用来折叠内容，提供了折叠显示的功能。

```html
<details>
这是一段解释文本。
</details>
```

上面的代码在浏览器里面，会折叠起来，显示`Details`，前面有一个三角形，就像下面这样。

```html
▶ Details
```

用户点击这段文本，折叠的文本就会展开，显示详细内容。

```html
▼ Details
这是一段解释文本。
```

再点击一下，展开的文本又会重新折叠起来。

`<summary>`标签用来定制折叠内容的标题。

```html
<details>
<summary>这是标题</summary>
这是一段解释文本。
</details>
```

上面的代码显示结果如下。

```html
▶ 这是标题
```

点击后，展示的效果如下。

```html
▼ 这是标题
这是一段解释文本。
```
