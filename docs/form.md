# 表单

表单（form）是用户输入信息，与网页互动的一种形式。大多数情况下，用户提交的信息会发给服务器，比如网站的搜索栏就是表单。

表单由一种或多种的小部件组成，比如输入框、按钮、单选框或复选框。这些小部件称为控件（controls）。

## `<form>`

`<form>`标签用来定义一个表单，所有表单内容放到这个容器元素之中。

```html
<form>
  <!-- 各种表单控件-->
</form>
```

上面代码就是表单的基本形式。

`<form>`有以下属性。

- `accept-charset`：服务器接受的字符编码列表，使用空格分隔，默认与网页编码相同。
- `action`：服务器接收数据的 URL。
- `autocomplete`：如果用户没有填写某个控件，浏览器是否可以自动填写该值。它的可能取值分别为`off`（不自动填写）和`on`（自动填写）。
- `method`：提交数据的 HTTP 方法，可能的值有`post`（表单数据作为 HTTP 数据体发送），`get`（表单数据作为 URL 的查询字符串发送），`dialog`（表单位于`<dialog>`内部使用）。
- `enctype`：当`method`属性等于`post`时，该属性指定提交给服务器的 MIME。可能的值为`application/x-www-form-urlencoded`（默认值），`multipart/form-data`（文件上传的情况），`text/plain`。
- `name`：表单的名称，应该在网页中是唯一的。
- `novalidate`：布尔属性，表单提交时是否取消验证。
- `target`：在哪个窗口展示服务器返回的数据，可能的值有`_self`（当前窗口），`_blank`（新建窗口），`_parent`（父窗口），`_top`（顶层窗口），`<iframe>`标签的`name`属性（即表单返回结果展示在`<iframe>`窗口）。

下面是一个比较常见的例子。

```html
<form action="https://example.com/api" method="post">
  <label for="POST-name">Name:</label>
  <input id="POST-name" type="text" name="name">
  <input type="submit" value="Save">
</form>
```

上面代码表示将一个`name`控件的值，使用`POST`方法发送到服务器网址`https://example.com/api`。

## `<fieldset>`，`<legend>`

`<fieldset>`标签是一个块级容器标签，表示控件的集合，用于将一组相关控件组合成一组。

```html
<form>
  <fieldset>
    <p>年龄：<input type="text" name="age"></p>
    <p>性别：<input type="text" name="gender"></p>
  </fieldset>
</form>
```

上面代码中，两个输入框是一组，它们的外面会显示一个方框。

`<fieldset>`有以下属性。

- `disabled`：布尔属性，一旦设置会使得`<fieldset>`内部包含的控件都不可用，都变成灰色状态。
- `form`：指定控件组所属的`<form>`，它的值等于`<form>`的`id`属性。
- `name`：该控件组的名称。

`<legend>`标签用来设置`<fieldset>`控件组的标题，通常是`<fieldset>`内部的第一个元素，会嵌入显示在控件组的上边框里面。

```html
<fieldset>
  <legend>学生情况登记</legend>
  <p>年龄：<input type="text" name="age"></p>
  <p>性别：<input type="text" name="gender"></p>
</fieldset>
```

上面代码中，这个控件组的标题会，嵌入显示在`<fieldset>`的上边框。

## `<input>`

### type 属性

`type`属性指定输入框的类型。不同类型的输入框，对输入会产生不同的限制。

- `email`：只能输入电子邮件地址。
- `number`：只能输入数值。
- `url`：只能输入网址。注意，不带有协议的网址是无效的，比如`foo.com`是无效的，`http://foo.com`是有效的。
- `tel`：只能输入电话号码，由于全世界的电话号码格式都不相同，因此这个类型不是很有用，大多数时候需要自定义验证。

### minlength 属性，maxlength 属性

`minlength`属性指定输入框内容的最小长度，`maxlength`属性指定最大长度。

```html
<input type="text" id="uname" name="uname" minlength="4" maxlength="10">
```

### min 属性，max 属性

`min`属性指定输入框内容的最小值，`max`属性指定最大值。通常，这两个属性与`number`类型配合使用。

```html
<input type="number" id="age" name="age" min="10" max="80" placeholder="30">
```

### pattern 属性

`pattern`属性的值是一个正则表达式，确保输入框的内容符合这个表达式。

```html
<input type="text" id="uname" name="uname" pattern="[a-zA-Z0-9]+">
```

这个属性可以与`email`或`url`等类型结合使用，限制用户只能填入某些域的值。

```html
<input type="email" id="email" pattern=".+@foo.com|.+@bar.com">
```

上面代码限制邮件地址只是属于`foo.com`或`bar.com`。

### required 属性

`required`属性表示这个表单项是必填的。

```html
<input id="email" type="email" required>
```

### placeholder 属性

`placeholder`属性指定输入框的占位符。

```html
<input type="number" id="age" name="age" min="10" max="80" placeholder="30">
```

### formaction 属性

input元素有`formaction`属性，用来强制当前表单跳转到指定的 URL，而不是表单的`action`属性指定的URL。

```html
<form action="http://e1.com">
  <input type=submit value=Submit ↵
     formaction="http://e2.com">
</form>
```

上面代码中，如果点击提交按钮，表单会跳转到`e2.com`，而不是`e1.com`。它的主要用途是一个表单可以提交到多个目的地。

该属性对具有提交作用的元素都有效，比如`<input type=submit>`、`<input type=image>`和`<button>`。

## encrypt 属性

`<form>`表单的`encrypt`属性，指定了表单数据提交到服务器的`content type`类型。这个属性可以取以下类型的值。

> - `application/x-www-form-urlencoded`：默认类型，控件名和控件值都要转义（空格转为加号，非数字和非字母转为%HH的形式，换行转为CR LF），控件名和控件值之间用等号分隔。控件按照出现顺序排列，控件之间用&分隔。
> - `multipart/form-data`：主要用于提交文件、非ASCII字符和二进制数据。这个类型用于提交大文件时，会将文件分成多块传送，每一块的HTTP头信息都有Content-Disposition属性，值为form-data，以及一个name属性，值为控件名。

```bash
Content-Disposition: form-data; name="mycontrol"
```

下面是上传文件的表单。

```html
<FORM action="http://server.com/cgi/handle"
       enctype="multipart/form-data"
       method="post">
   <P>
   What is your name? <INPUT type="text" name="submit-name"><BR>
   What files are you sending? <INPUT type="file" name="files"><BR>
   <INPUT type="submit" value="Send"> <INPUT type="reset">
 </FORM>
```

实际发送的数据格式如下。

```html
Content-Type: multipart/form-data; boundary=AaB03x

   --AaB03x
   Content-Disposition: form-data; name="submit-name"

   Larry
   --AaB03x
   Content-Disposition: form-data; name="files"; filename="file1.txt"
   Content-Type: text/plain

   ... contents of file1.txt ...
   --AaB03x--
```

## `<button>`

`<button>`标签会生成一个可以点击的按钮。

```html
<button>搜索</button>
```

上面代码会产生一个按钮，上面的文字就是“搜索”。

`<button>`具有以下属性。

- `autofocus`：布尔属性，表示网页加载时，焦点就在这个按钮。网页里面只能有一个元素，具有这个属性。
- `disabled`：布尔属性，表示按钮不可用，会导致按钮变灰，不可点击。
- `name`：按钮的名称（与`value`属性配合使用），将以`name=value`的形式，随表单一起提交到服务器。
- `value`：按钮的值（与`name`属性配合使用），将以`name=value`的形式，随表单一起提交到服务器。
- `type`：按钮的类型，可能的值有三种：`submit`（点击后将数据提交给服务器），`reset`（将所有控件的值重置为初始值），`button`（没有默认行为，由脚本指定按钮的行为）。
- `form`：指定按钮关联的`<form>`表单，值为`<form>`的`id`属性。如果省略该属性，默认关联按钮所在父表单。
- `formaction`：数据提交到服务器的目标 URL，会覆盖`<form>`元素的`action`属性。
- `formenctype`：数据提交到服务器的编码方式，会覆盖`<form>`元素的`enctype`属性。可能的值有三种：`application/x-www-form-urlencoded`（默认值），`multipart/form-data`（只用于文件上传），`text/plain`。
- `formmethod`：数据提交到服务器使用的 HTTP 方法，会覆盖`<form>`元素的`method`属性，可能的值为`post`或`get`。
- `formnovalidate`：布尔属性，数据提交到服务器时关闭本地验证，会覆盖`<form>`元素的`novalidate`属性。
- `formtarget`：数据提交到服务器后，展示服务器返回数据的窗口，会覆盖`<form>`元素的`target`属性。可能的值有`_self`（当前窗口），`_blank`（新的空窗口）、`_parent`（父窗口）、`_top`（顶层窗口）。

`<button>`内部不仅放置文字，还可以放置图像，这可以形成图像按钮。

```html
<button name="search" type="submit">
  <img src="search.gif">搜索
</button>
```

### `<label>`

`<label>`标签提供控件的文字说明，帮助用户理解控件的目的。



## 表单的校验规则

HTML5 允许在表单元素的属性里面，指定该元素的校验规则。

```html
<!-- 必填 -->
<input type="text" required>
<input type="checkbox" required>
<input type="radio" name="myradiogroup1" required>
<input type="file" required>
<input type="email" value="invalid" required>
<input type="url" value="invalid" required>
<select required>

<!-- 指定输入模式 -->
<input type="text" value="1" pattern="[a-z]" required>

<!-- 指定输入字符的最少个数和最多个数 -->
<input type="text" minlength=100 required>
<input type="text" maxlength=1 required>

<!-- 指定输入的最小值和最大值 -->
<input type="number" value="1" min=5 required>
<input type="number" value="10" max=5 required>

<!-- 指定步长 -->
<input type="number" value="10" min=0 step=3 required>
```

表单元素的`setCustomValidity`方法，用来自定义校验失败的报错信息。

```javascript
// HTML 代码为
// <input type="text" id="customValidityInput">
document
.getElementById('customValidityInput')
.setCustomValidity('表单校验失败')
```

下面是另一个例子。

```html
<label for="feeling">Feeling:</label>
<input id="feeling" type="text" oninput="validateFeeling(this)">
<script>
 function validateFeeling(input) {
   if (input.value == "good" || input.value == "fine" || input.value == "tired") {
     input.setCustomValidity('"' + input.value + '" is not a feeling');
   } else {
     // The data is valid, reset the error message.
     input.setCustomValidity('');
   }
 }
</script>
```

## 参考链接

- [HTML Interactive Form Validation](https://webkit.org/blog/7099/html-interactive-form-validation/), by Chris Dumez

