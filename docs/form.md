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

下面是一个比较常见的例子。

```html
<form action="https://example.com/api" method="post">
  <label for="POST-name">用户名：</label>
  <input id="POST-name" type="text" name="name">
  <input type="submit" value="提交">
</form>
```

上面代码会显示一个用户名输入框和一个提交按钮。用户在输入框内部输入用户名，比如`foobar`，然后点击提交按钮，浏览器就会向服务器`https://example.com/api`发送一个 POST 请求，发送`name=foobar`这样一段数据。

`<form>`有以下属性。

- `accept-charset`：服务器接受的字符编码列表，使用空格分隔，默认与网页编码相同。
- `action`：服务器接收数据的 URL。
- `autocomplete`：如果用户没有填写某个控件，浏览器是否可以自动填写该值。它的可能取值分别为`off`（不自动填写）和`on`（自动填写）。
- `method`：提交数据的 HTTP 方法，可能的值有`post`（表单数据作为 HTTP 数据体发送），`get`（表单数据作为 URL 的查询字符串发送），`dialog`（表单位于`<dialog>`内部使用）。
- `enctype`：当`method`属性等于`post`时，该属性指定提交给服务器的 MIME。可能的值为`application/x-www-form-urlencoded`（默认值），`multipart/form-data`（文件上传的情况），`text/plain`。
- `name`：表单的名称，应该在网页中是唯一的。
- `novalidate`：布尔属性，表单提交时是否取消验证。
- `target`：在哪个窗口展示服务器返回的数据，可能的值有`_self`（当前窗口），`_blank`（新建窗口），`_parent`（父窗口），`_top`（顶层窗口），`<iframe>`标签的`name`属性（即表单返回结果展示在`<iframe>`窗口）。

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

### 类型

`<input>`标签是用来接收用户输入的一种控件，它是一个单独使用的标签，没有结束标志。

它有多种形式，取决于`type`属性的值，默认值是`text`，表示一个输入框。

```html
<input type="text">
```

上面代码会生成一个输入框，占据一行，用户可以在里面输入文本。

`type`属性决定了`<input>`的形式。该属性可以取以下值。

**（1）text**

`type="text"`是普通的文本输入框，用来输入单行文本。如果用户输入换行符，换行符会自动从输入中删除。

```html
<input type="text" id="name" name="name" required
       minlength="4" maxlength="8" size="10">
```

`text`输入框有以下配套属性。

- `maxlength`：可以输入的最大字符数，值为一个非负整数。
- `minlength`：可以输入的最小字符数，值为一个非负整数，且必须小于`maxlength`。
- `pattern`：用户输入必须匹配的正则表达式，比如要求用户输入4个～8个英文字符，可以写成`pattern="[a-z]{4,8}"`。
- `placeholder`：输入字段为空时，用于提示的示例值。只要用户没有任何字符，该提示就会出现，否则会消失。
- `readonly`：布尔属性，表示该输入框是只读的，用户只能看，不能输入。
- `size`：表示输入框的显示长度有多少个字符宽，它的值是一个正整数，默认等于20。超过这个数字的字符，必须移动光标才能看到。
- `spellcheck`：是否对用户输入启用拼写检查，可能的值为`true`或`false`。

**（2）button**

`type="button"`是没有默认行为的按钮，通常脚本指定`click`事件的监听函数来使用。

```html
<input type="button" value="点击">
```

建议尽量不使用这个类型，而使用`<button>`标签代替，一则语义更清晰，二则`<button>`标签内部可以插入图片或其他 HTML 代码。

**（3）submit**

`type="submit"`是表单的提交按钮。用户点击这个按钮，就会把表单提交给服务器。

```html
<input type="submit" value="提交">
```

如果不指定`value`属性，浏览器会在提交按钮上显示默认的文字，通常是`Submit`。

该类型有以下配套属性，用来覆盖`<form>`标签的相应设置。

- `formaction`：提交表单数据的服务器 URL。
- `formenctype`：表单数据的编码类型。
- `formmethod`：提交表单使用的 HTTP 方法（`get`或`post`）。
- `formnovalidate`：一个布尔值，表示数据提交给服务器之前，是否要忽略表单验证。
- `formtarget`：收到服务器返回的数据后，在哪一个窗口显示。

**（4）image**

`type="image"`表示将一个图像文件作为提交按钮，行为和用法与`type="submit"`完全一致。

```html
<input type="image" alt="登陆" src="login-button.png">
```

上面代码中，图像文件是一个可以点击的按钮，点击后会提交数据到服务器。

该类型有以下配套属性。

- `alt`：图像无法加载时显示的替代字符串。
- `src`：加载的图像 URL。
- `height`：图像的显示高度，单位为像素。
- `width`：图像的显示宽度，单位为像素。
- `formaction`：提交表单数据的服务器 URL。
- `formenctype`：表单数据的编码类型。
- `formmethod`：提交表单使用的 HTTP 方法（`get`或`post`）。
- `formnovalidate`：一个布尔值，表示数据提交给服务器之前，是否要忽略表单验证。
- `formtarget`：收到服务器返回的数据后，在哪一个窗口显示。

用户点击图像按钮提交时，会额外提交两个参数`x`和`y`到服务器，表示鼠标的点击位置，比如`x=52&y=55`。`x`是横坐标，`y`是纵坐标，都以图像左上角作为原点`(0, 0)`。如果图像按钮设置了`name`属性，比如`name="position"`，那么将以该值作为坐标的前缀，比如`position.x=52&position.y=55`。这个功能通常用来地图类型的操作，让服务器知道用户点击了地图的哪个部分。

**（5）reset**

`type="reset"`是一个重置按钮，用户点击以后，所有表格控件重置为初始值。

```html
<input type="reset" value="重置">
```

如果不设置`value`属性，浏览器会在按钮上面加上默认文字，通常是`Reset`。

这个控件用处不大，用户点错了还会使得所有已经输入的值都被重置，建议不要使用。

**（6）checkbox**

`type="checkbox"`是复选框，允许选择或取消选择该选项。

```html
<input type="checkbox" name="agreement" checked>
<label for="agreement">是否同意</label>
```

上面代码会在文字前面，显示一个可以点击的选择框，点击可以选中，再次点击可以取消。上面代码中，`checked`属性表示默认选中。

`value`属性的默认值是`on`。也就是说，如果没有设置`value`属性，以上例来说，选中复选框时，会提交`agreement=on`。如果没有选中，提交时不会有该项。

多个相关的复选框，可以放在`<fieldset>`里面。

```html
<fieldset>
  <legend>你的兴趣</legend>
  <div>
    <input type="checkbox" id="coding" name="interest" value="coding">
    <label for="coding">编码</label>
  </div>
  <div>
    <input type="checkbox" id="music" name="interest" value="music">
    <label for="music">音乐</label>
  </div>
</fieldset>
```

上面代码中，如果用户同时选中两个复选框，提交的时候就会有两个`name`属性，比如`interest=coding&interest=music`。

**（7）radio**

`type="radio"`是单选框，表示一组选择之中，只能选中一项。单选框通常为一个小圆圈，选中时会被填充或突出显示。

```html
<fieldset>
  <legend>性别</legend>
  <div>
    <input type="radio" id="male" name="gender" value="male">
    <label for="male">男</label>
  </div>
  <div>
    <input type="radio" id="female" name="gender" value="female">
    <label for="female">女</label>
  </div>
</fieldset>
```

上面代码中，性别只能在两个选项之中，选择一项。

注意，多个单选框的`name`属性的值，应该都是一致的。提交到服务器的就是选中的那个值。

该类型的配套属性如下。

- `checked`：布尔属性，表示是否默认选中当前项。
- `value`：用户选中该项时，提交到服务器的值，默认为`on'`。

**（8）email**

`type="email"`是一个只能输入电子邮箱的文本输入框。表单提交之前，浏览器会自动验证是否符合电子邮箱的格式，如果不符合就会显示提示，无法提交到服务器。

```html
<input type="email" pattern=".+@foobar.com" size="30" required>
```

上面代码会生成一个必填的文本框，只能输入后缀为`foobar.com`的邮箱地址。

该类型有一个`multiple`的布尔属性，一旦设置，就表示该输入框可以输入多个逗号分隔的电子邮箱。

```html
<input id="emailAddress" type="email" multiple required>
```

注意，如果同时设置了`multiple`属性和`required`属性，零个电子邮箱是允许的，也就是该输入框允许为空。

该类型的配套属性如下。

- `maxlength`：可以输入的最大字符数。
- `minlength`：可以输入的最少字符数。
- `multiple`：布尔属性，是否允许输入多个以逗号分隔的电子邮箱。
- `pattern`：输入必须匹配的正则表达式。
- `placeholder`：输入为空时的显示文本。
- `readonly`：布尔属性，该输入框是否只读。
- `size`：一个非负整数，表示输入框的显示长度为多少个字符。
- `spellcheck`：是否对输入内容启用拼写检查，可能的值为`true`或`false`。

该类型还可以搭配`<datalist>`标签，提供输入的备选项。

```html
<input type="email" size="40" list="defaultEmails">

<datalist id="defaultEmails">
  <option value="jbond007@mi6.defence.gov.uk">
  <option value="jbourne@unknown.net">
  <option value="nfury@shield.org">
  <option value="tony@starkindustries.com">
  <option value="hulk@grrrrrrrr.arg">
</datalist>
```

上面代码中，输入焦点进入输入框以后，会显示一个下拉列表，里面有五个参考项，供用户参考。

**（9）password**

`type="password"`是一个密码输入框。用户的输入会被遮挡，字符通常显示星号（`*`）或点（`·`）。

```html
<input type="password" id="pass" name="password"
           minlength="8" required>
```

浏览器对该类型输入框的显示，会有所差异。一种常见的处理方法是，用户每输入一个字符，先在输入框里面显示一秒钟，然后再遮挡该字符。

如果用户输入内容包含换行符（`U+000A`）和回车符（`U+000D`），浏览器会自动将这两个字符过滤掉。

该类型的配套属性如下。

- `maxlength`：可以输入的最大字符数。
- `minlength`：可以输入的最少字符数。
- `pattern`：输入必须匹配的正则表达式。
- `placeholder`：输入为空时的显示文本。
- `readonly`：布尔属性，该输入框是否只读。
- `size`：一个非负整数，表示输入框的显示长度为多少个字符。
- `autocomplete`：是否允许自动填充，可能的值有`on`（允许自动填充）、`off`（不允许自动填充）、`current-password`（填入当前网站保存的密码）、`new-password`（自动生成一个随机密码）。
- `inputmode`：允许用户输入的数据类型，可能的值有`none`（不使用系统输入法）、`text`（标准文本输入）、`decimal`（数字，包含小数）、`numeric`（数字0-9）等。

**（10）file**

`type="file"`是一个文件选择框，允许用户选择一个或多个文件，常用于文件上传功能。

```html
<input type="file"
       id="avatar" name="avatar"
       accept="image/png, image/jpeg">
```

该类型有以下属性。

- `accept`：允许选择的文件类型，使用逗号分隔，可以使用 MIME 类型（比如`image/jpeg`），也可以使用后缀名（比如`.doc`），还可以使用`audio/*`（任何音频文件）、`video/*`（任何视频文件）、`image/*`（任何图像文件）等表示法。
- `capture`：用于捕获图像或视频数据的源，可能的值有`user`（面向用户的摄像头或麦克风），`environment`（外接的摄像头或麦克风）。
- `multiple`：布尔属性，是否允许用户选择多个文件。

**（11）hidden**

`type="hidden"`是一个不显示在页面的控件，用户无法输入它的值，主要用来向服务器传递一些隐藏信息。比如，CSRF 攻击会伪造表单数据，那么使用这个控件，可以为每个表单生成一个独一无二的隐藏编号，防止伪造表单提交。

```html
<input id="prodId" name="prodId" type="hidden" value="xm234jq">
```

上面这个控件，页面上是看不见的。用户提交表单的时候，浏览器会将`prodId=xm234jq`发给服务器。

**（12）number**

`type="number"`是一个数字输入框，只能输入数字。浏览器通常会在输入框的最右侧，显示一个可以点击的上下箭头，点击向上箭头，数字会递增，点击向下箭头，数字会递减。

```html
<input type="number" id="tentacles" name="tentacles"
       min="10" max="100">
```

上面代码指定数字输入框，最小可以输入10，最大可以输入100。

该类型可以接受任何数值，包括小数和整数。可以通过`step`属性，限定只接受整数。

该类型有以下配套属性。

- `max`：允许输入的最大数值。
- `min`：允许输入的最小数值。
- `placeholder`：用户输入为空时，显示的示例值。
- `readonly`：布尔属性，表示该控件是否为只读。
- `step`：点击向上和向下箭头时，数值每次递减的步长值。如果用户输入的值，不符合步长值的设定，浏览器会自动四舍五入到最近似的值。默认的步长值是`1`，如果初始的`value`属性设为`1.5`，那么点击向上箭头得到`2.5`，点击向下箭头得到`0.5`。

**（13）range**

- `color`：选择颜色的控件。
- `date`：选择年月日的控件。
- `datetime-local`：选择日期和时间的控件，没有时区。
- `month`：输入月份和年份的控件，没有时区。
- `range`：允许用户在某个范围内进行选择的控件。
- `time`：输入时间的控件，没有时区。
- `url`：只能输入网址的输入框。注意，不带有协议的网址是无效的，比如`foo.com`是无效的，`http://foo.com`是有效的。
- `tel`：只能输入电话号码的输入框。由于全世界的电话号码格式都不相同，因此这个类型不是很有用，大多数时候需要自定义验证。
- `week`：输入日期的控件，只能输入年数和周数，没有时区。

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

## `<label>`

`<label>`标签提供控件的文字说明，帮助用户理解控件的目的。

## `<datalist>`，`<option>`

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

