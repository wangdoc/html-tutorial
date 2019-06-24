<dialog> 元素

## 简介

各种前端框架都提供对话框功能，HTML 5.2 引入了`<dialog>`元素，将这个功能标准化了，表示一个可以关闭的对话框。

```html
<dialog>
  Hello world
</dialog>
```

上面就是一个最简单的对话框。

`<dialog>`元素里面，也可以放入其他 HTML 元素。

```html
<dialog>
  <form method="dialog">
    <input type="text">
    <button type="submit">SUBMIT</button>
  </form>
</dialog>
```

上面的对话框里面，有一个输入框和提交按钮。

默认情况下，对话框是隐藏的，不会在网页上显示。如果要让对话框显示，必须加上`open`属性。

```html
<dialog open>
  <form method="dialog">
    <input type="text">
    <button type="submit">SUBMIT</button>
  </form>
</dialog>
```

上面代码中，`<dialog>`打开了`open`属性，这个对话框就可见了，表示处于打开状态。另外，`<form>`的`method`属性设为`dialog`，这时点击提交按钮，对话框就会消失。

## API

`<dialog>`元素的 JavaScript API 提供`showModal()`和`close()`两个方法，用于打开/关闭对话框。

```javascript
const modal = document.querySelector('dialog');

// 对话框显示，相当于增加 open 属性
modal.showModal();

// 对话框关闭，相当于移除 open 属性
modal.close();
```

开发者可以提供关闭按钮，让其调用`close()`方法，关闭对话框。

`close()`方法可以接受一个字符串作为参数，用于传递信息。`<dialog>`接口的`returnValue`属性可以读取这个字符串。

```javascript
modal.close('Accepted');
modal.returnValue // "Accepted"
```

`showModal()`方法唤起对话框时，会有一个透明层，阻止用户与对话框外部的内容互动。可以编写 CSS，让透明层变得可见。

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

`dialog`元素还有一个`show()`方法，也能唤起对话框，但是没有透明层，用户可以与对话框外部的内容互动。

## 事件

`dialog`元素有两个事件，可以监听。

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

## 参考链接

- [Meet the New Dialog Element](https://keithjgrant.com/posts/2018/meet-the-new-dialog-element/), Keith J. Grant
- [The dialog element: The way to create tomorrow’s modal windows](https://blog.logrocket.com/the-dialog-element-the-way-to-create-tomorrows-modal-windows-f1d4ab14380b), Abhishek Jakhar
