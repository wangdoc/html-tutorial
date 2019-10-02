# 其他标签

本章介绍一些最新引入标准的标签。

## `<dialog>`

### 基本用法

`<dialog>`标签表示一个可以关闭的对话框。

```html
<dialog>
  Hello world
</dialog>
```

上面就是一个最简单的对话框。

默认情况下，对话框是隐藏的，不会在网页上显示。如果要让对话框显示，必须加上`open`属性。

```html
<dialog open>
  Hello world
</dialog>
```

上面代码会在网页显示一个方框，内容是`Hello world`。

`<dialog>`元素里面，可以放入其他 HTML 元素。

```html
<dialog open>
  <form method="dialog">
    <input type="text">
    <button type="submit" value="foo">提交</button>
  </form>
</dialog>
```

上面的对话框里面，有一个输入框和提交按钮。

注意，上例中`<form>`的`method`属性设为`dialog`，这时点击提交按钮，对话框就会消失。但是，表单不会提交到服务器，浏览器会将表单元素的`returnValue`属性设为 Submit 按钮的`value`属性（上例是`foo`）。

### JavaScript API

`<dialog>`元素的 JavaScript API 提供`Dialog.showModal()`和`Dialog.close()`两个方法，用于打开/关闭对话框。

```javascript
const modal = document.querySelector('dialog');

// 对话框显示，相当于增加 open 属性
modal.showModal();

// 对话框关闭，相当于移除 open 属性
modal.close();
```

开发者可以提供关闭按钮，让其调用`Dialog.close()`方法，关闭对话框。

`Dialog.close()`方法可以接受一个字符串作为参数，用于传递信息。`<dialog>`接口的`returnValue`属性可以读取这个字符串，否则`returnValue`属性等于提交按钮的`value`属性。

```javascript
modal.close('Accepted');
modal.returnValue // "Accepted"
```

`Dialog.showModal()`方法唤起对话框时，会有一个透明层，阻止用户与对话框外部的内容互动。CSS 提供了一个 Dialog 元素的`::backdrop`伪类，用于选中这个透明层，因此可以编写样式让透明层变得可见。

```css
dialog {
  padding: 0;
  border: 0;
  border-radius: 0.6rem;
  box-shadow: 0 0 1em black;
}

dialog::backdrop {
  /* make the backdrop a semi-transparent black */
  background-color: rgba(0, 0, 0, 0.4);
}
```

上面代码不仅为`<dialog>`指定了样式，还将对话框的透明层变成了灰色透明。

`<dialog>`元素还有一个`Dialog.show()`方法，也能唤起对话框，但是没有透明层，用户可以与对话框外部的内容互动。

### 事件

`<dialog>`元素有两个事件，可以监听。

- `close`：对话框关闭时触发
- `cancel`：用户按下`esc`键关闭对话框时触发

如果希望用户点击透明层，就关闭对话框，可以用下面的代码。

```javascript
modal.addEventListener('click', (event) => {
  if (event.target === modal) {
    modal.close('cancelled');
  }
});
```

## `<details>`，`<summary>`

### 基本用法

`<details>`标签用来折叠内容，浏览器会折叠显示该标签的内容。

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

`<details>`标签的`open`属性，用于默认打开折叠。

```html
<details open>
这是一段解释文本。
</details>
```

上面代码默认打开折叠。

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

通过 CSS 设置`summary::-webkit-details-marker`，可以改变标题前面的三角箭头。

```css
summary::-webkit-details-marker {
  background: url(https://example.com/foo.svg);
  color: transparent;
}
```

下面的样式是另一种替换箭头的方法。

```css
summary::-webkit-details-marker {
  display: none;
}
summary:before {
  content: "\2714";
  color: #696f7c;
  margin-right: 5px;
}
```


### JavaScript API

`Details`元素的`open`属性返回`<details>`当前是打开还是关闭。

```javascript
const details = document.querySelector('details');

if (detail.open === true) {
  // 展开状态
} else {
  // 折叠状态
}
```

`Details`元素有一个`toggle`事件，打开或关闭折叠时，都会触发这个事件。

```javascript
details.addEventListener('toggle', event => {
  if (details.open) {
    /* 展开状况 */
  } else {
    /* 折叠状态 */
  }
});
```

## 参考链接

- [Meet the New Dialog Element](https://keithjgrant.com/posts/2018/meet-the-new-dialog-element/), Keith J. Grant
- [The dialog element: The way to create tomorrow’s modal windows](https://blog.logrocket.com/the-dialog-element-the-way-to-create-tomorrows-modal-windows-f1d4ab14380b), Abhishek Jakhar
- [Details/Summary is the Easiest Way Ever to Make an Accordion](https://css-tricks.com/quick-reminder-that-details-summary-is-the-easiest-way-ever-to-make-an-accordion/), Chris Coyier

