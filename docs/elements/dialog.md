# <dialog> 元素

HTML 5.2 引入了`<dialog>`元素，表示一个可以关闭的对话框。

```html
<dialog open>
  Native dialog box!
</dialog>
```

上面代码中，`open`属性表示这个对话框默认是打开的，否则是关闭的。

`<dialog>`元素内部可以自定义内容。

```html
<dialog id="demo-modal">
  <h3 class="modal-header">标题</h3>
  <div class="modal-body">
    <p>xxx</p>
  </div>
  <footer class="modal-footer">
    <button id="close" type="button">关闭</button>
  </footer>
</dialog>
```

JavaScript 的`<dialog>`接口提供`showModal`和`close`两个方法，用于打开/关闭对话框。

```javascript
const modal = document.querySelector('dialog');

// makes modal appear (adds `open` attribute)
modal.showModal();

// hides modal (removes `open` attribute)
modal.close();
```

按下`esc`键会关闭对话框，但是开发者也可以设置关闭按钮，调用`close`方法。

`close`方法可以接受一个字符串作为参数，用于传递信息。`<dialog>`接口的`returnValue`属性可以读取这个字符串。

```javascript
modal.close('Accepted');
modal.returnValue // "Accepted"
```

`showModal`方法唤起对话框时，会有一个透明层，阻止用户与对话框外部的内容互动。可以编写 CSS，让透明层变得可见。

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

`dialog`元素还有一个`show`方法，也能唤起对话框，但是没有透明层，用户可以与对话框外部的内容互动。

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

- [Meet the New Dialog Element](https://keithjgrant.com/posts/2018/meet-the-new-dialog-element/), by Keith J. Grant
