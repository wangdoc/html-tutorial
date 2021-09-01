# 表单标签

表单（form）是用户输入信息与网页互动的一种形式。大多数情况下，用户提交的信息会发给服务器，比如网站的搜索栏就是表单。

表单由一种或多种的小部件组成，比如输入框、按钮、单选框或复选框。这些小部件称为控件（controls）。

## `<form>`

### 简介

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
  <input id="POST-name" type="text" name="user">
  <input type="submit" value="提交">
</form>
```

上面代码就是一个表单，一共包含三个控件：一个`<label>`标签，一个文本输入框，一个提交按钮。其中，文本输入框的`name`属性是`user`，表示将向服务器发送一个键名为`user`的键值对，键值就是这个控件的`value`属性，等于用户输入的值。

用户在文本输入框里面，输入用户名，比如`foobar`，然后点击提交按钮，浏览器就会向服务器`https://example.com/api`发送一个 POST 请求，发送`user=foobar`这样一段数据。

`<form>`有以下属性。

- `accept-charset`：服务器接受的字符编码列表，使用空格分隔，默认与网页编码相同。
- `action`：服务器接收数据的 URL。
- `autocomplete`：如果用户没有填写某个控件，浏览器是否可以自动填写该值。它的可能取值分别为`off`（不自动填写）和`on`（自动填写）。
- `method`：提交数据的 HTTP 方法，可能的值有`post`（表单数据作为 HTTP 数据体发送），`get`（表单数据作为 URL 的查询字符串发送），`dialog`（表单位于`<dialog>`内部使用）。
- `enctype`：当`method`属性等于`post`时，该属性指定提交给服务器的 MIME 类型。可能的值为`application/x-www-form-urlencoded`（默认值），`multipart/form-data`（文件上传的情况），`text/plain`。
- `name`：表单的名称，应该在网页中是唯一的。注意，如果一个控件没有设置`name`属性，那么这个控件的值就不会作为键值对，向服务器发送。
- `novalidate`：布尔属性，表单提交时是否取消验证。
- `target`：在哪个窗口展示服务器返回的数据，可能的值有`_self`（当前窗口），`_blank`（新建窗口），`_parent`（父窗口），`_top`（顶层窗口），`<iframe>`标签的`name`属性（即表单返回结果展示在`<iframe>`窗口）。

### enctype 属性

`<form>`表单的`enctype`属性，指定了采用 POST 方法提交数据时，浏览器给出的数据的 MIME 类型。该属性可以取以下值。

（1）`application/x-www-form-urlencoded`

`application/x-www-form-urlencoded`是默认类型，控件名和控件值都要转义（空格转为`+`号，非数字和非字母转为`%HH`的形式，换行转为CR LF），控件名和控件值之间用`=`分隔。控件按照出现顺序排列，控件之间用`&`分隔。

（2）`multipart/form-data`

`multipart/form-data`主要用于文件上传。这个类型上传大文件时，会将文件分成多块传送，每一块的 HTTP 头信息都有`Content-Disposition`属性，值为`form-data`，以及一个`name`属性，值为控件名。

```bash
Content-Disposition: form-data; name="mycontrol"
```

下面是上传文件的表单。

```html
<form action="https://example.com/api"
      enctype="multipart/form-data"
      method="post">
  用户名：<input type="text" name="submit-name"><br>
  文件：<input type="file" name="files"><br>
  <input type="submit" value="上传"> <input type="reset" value="清除">
</form>
```

上面代码中，输入用户名`Larry`，选中一个`file1.txt`文件，然后点击“上传”。浏览器发送的实际数据如下。

```http
Content-Type: multipart/form-data; boundary=--AaB03x

--AaB03x
Content-Disposition: form-data; name="submit-name"

Larry
--AaB03x
Content-Disposition: form-data; name="files"; filename="file1.txt"
Content-Type: text/plain

... contents of file1.txt ...
--AaB03x--
```

上面代码中，浏览器将这个表单发成多个数据块。最上面使用`Content-Type`字段告诉服务器，数据格式是`multipart/form-data`（即多个数据块），每个数据块的分隔标志是`--AaB03x`。每个数据块的第一行是`Content-Disposition`，其中的`name`字段表示这个数据块的控件名，数据体则是该控件的数据值，比如第一个数据块的`name`属性是`submit-name`控件，数据体是该控件的值`Larry`。第二个数据块是控件`files`，由于该控件是上传文件，所以还要用`filename`属性给出文件名`file1.txt`，数据体是`file1.txt`的内容。

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

## `<label>`

`<label>`标签是一个行内元素，提供控件的文字说明，帮助用户理解控件的目的。

```html
<label for="user">用户名：</label>
<input type="text" name="user" id="user">
```

上面代码中，输入框前面会有文字说明“用户名：”。

`<label>`的一大优势是增加了控件的可用性。有些控件比较小（比如单选框），不容易点击，那么点击对应的`<label>`标签，也能选中该控件。点击`<label>`，就相当于控件本身的`click`事件。

`<label>`的`for`属性关联相对应的控件，它的值是对应控件的`id`属性。所以，控件最好设置`id`属性。

控件也可以放在`<label>`之中，这时不需要`for`属性和`id`属性。

```html
<label>用户名：
  <input type="text" name="user">
</label>
```

`<label>`的属性如下。

- `for`：关联控件的`id`属性。
- `form`：关联表单的`id`属性。设置了该属性后，`<label>`可以放置在页面的任何位置，否则只能放在`<form>`内部。

一个控件可以有多个关联的`<label>`标签。

```html
<label for="username">用户名：</label>
<input type="text" id="username" name="username">
<label for="username"><abbr title="required">*</abbr></label>
```

上面代码中，`<input>`有两个关联的`<label>`。

## `<input>`

### 简介

`<input>`标签是一个行内元素，用来接收用户的输入。它是一个单独使用的标签，没有结束标志。

它有多种类型，取决于`type`属性的值，默认值是`text`，表示一个输入框。

```html
<input>
<!-- 等同于 -->
<input type="text">
```

上面代码会生成一个单行的输入框，用户可以在里面输入文本。

`<input>`的属性非常多，有些属性是某个类型专用的，放在下文的“类型”部分介绍。这里介绍一些所有类型的共同属性。

- `autofocus`：布尔属性，是否在页面加载时自动获得焦点。
- `disabled`：布尔属性，是否禁用该控件。一旦设置，该控件将变灰，用户可以看到，但是无法操作。
- `form`：关联表单的`id`属性。设置了该属性后，控件可以放置在页面的任何位置，否则只能放在`<form>`内部。
- `list`：关联的`<datalist>`的`id`属性，设置该控件相关的数据列表，详见后文。
- `name`：控件的名称，主要用于向服务器提交数据时，控件键值对的键名。注意，只有设置了`name`属性的控件，才会向服务器提交，不设置就不会提交。
- `readonly`：布尔属性，是否为只读。
- `required`：布尔属性，是否为必填。
- `type`：控件类型，详见下文。
- `value`：控件的值。

### 类型

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
- `pattern`：用户输入必须匹配的正则表达式，比如要求用户输入4个～8个英文字符，可以写成`pattern="[a-z]{4,8}"`。如果用户输入不符合要求，浏览器会弹出提示，不会提交表单。
- `placeholder`：输入字段为空时，用于提示的示例值。只要用户没有任何字符，该提示就会出现，否则会消失。
- `readonly`：布尔属性，表示该输入框是只读的，用户只能看，不能输入。
- `size`：表示输入框的显示长度有多少个字符宽，它的值是一个正整数，默认等于20。超过这个数字的字符，必须移动光标才能看到。
- `spellcheck`：是否对用户输入启用拼写检查，可能的值为`true`或`false`。

**（2）search**

`type="search"`是一个用于搜索的文本输入框，基本等同于`type="text"`。某些浏览器会在输入的时候，在输入框的尾部显示一个删除按钮，点击就会删除所有输入，让用户从头开始输入。

下面是一个例子。

```html
<form>
  <input type="search" id="mySearch" name="q"
    placeholder="输入搜索词……" required>
  <input type="submit" value="搜索">
</form>
```

**（3）button**

`type="button"`是没有默认行为的按钮，通常脚本指定`click`事件的监听函数来使用。

```html
<input type="button" value="点击">
```

建议尽量不使用这个类型，而使用`<button>`标签代替，一则语义更清晰，二则`<button>`标签内部可以插入图片或其他 HTML 代码。

**（4）submit**

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

**（5）image**

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

**（6）reset**

`type="reset"`是一个重置按钮，用户点击以后，所有表格控件重置为初始值。

```html
<input type="reset" value="重置">
```

如果不设置`value`属性，浏览器会在按钮上面加上默认文字，通常是`Reset`。

这个控件用处不大，用户点错了还会使得所有已经输入的值都被重置，建议不要使用。

**（7）checkbox**

`type="checkbox"`是复选框，允许选择或取消选择该选项。

```html
<input type="checkbox" id="agreement" name="agreement" checked>
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

**（8）radio**

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
- `value`：用户选中该项时，提交到服务器的值，默认为`on`。

**（9）email**

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

**（10）password**

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

**（11）file**

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

**（12）hidden**

`type="hidden"`是一个不显示在页面的控件，用户无法输入它的值，主要用来向服务器传递一些隐藏信息。比如，CSRF 攻击会伪造表单数据，那么使用这个控件，可以为每个表单生成一个独一无二的隐藏编号，防止伪造表单提交。

```html
<input id="prodId" name="prodId" type="hidden" value="xm234jq">
```

上面这个控件，页面上是看不见的。用户提交表单的时候，浏览器会将`prodId=xm234jq`发给服务器。

**（13）number**

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

**（14）range**

`type="range"`是一个滑块，用户拖动滑块，选择给定范围之中的一个数值。因为拖动产生的值是不精确的，如果需要精确数值，不建议使用这个控件。常见的例子是调节音量。

```html
<input type="range" id="start" name="volume"
         min="0" max="11">
```

上面代码会产生一个最小值为`0`、最大值为`11`的滑块区域。用户拖动滑块，选择想要的音量。

该类型的配套属性如下，用法与`type="number"`一致。

- `max`：允许的最大值，默认为100。
- `min`：允许的最小值，默认为0。
- `step`：步长值，默认为1。

`value`属性的初始值就是滑块的默认位置。如果没有设置`value`属性，滑块默认就会停在最大值和最小值中间。如果`max`属性、`min`属性、`value`属性都没有设置，那么`value`属性为50。

该类型与`<datalist>`标签配合使用，可以在滑动区域产生刻度。

```html
<input type="range" list="tickmarks">

<datalist id="tickmarks">
  <option value="0" label="0%">
  <option value="10">
  <option value="20">
  <option value="30">
  <option value="40">
  <option value="50" label="50%">
  <option value="60">
  <option value="70">
  <option value="80">
  <option value="90">
  <option value="100" label="100%">
</datalist>
```

上面代码会在0～100之间产生11个刻度。其中，`0%`、`50%`和`100%`三个位置会有文字提示，不过浏览器很可能不支持。

注意，浏览器生成的都是水平滑块。如果想要生成垂直滑块，可以使用 CSS 改变滑块区域的方向。

**（15）url**

`type="url"`是一个只能输入网址的文本框。提交表单之前，浏览器会自动检查网址格式是否正确，如果不正确，就会无法提交。

```html
<input type="url" name="url" id="url"
       placeholder="https://example.com"
       pattern="https://.*" size="30"
       required>
```

上面代码的`pattern`属性指定输入的网址只能使用 HTTPS 协议。

注意，该类型规定，不带有协议的网址是无效的，比如`foo.com`是无效的，`http://foo.com`是有效的。

该类型的配套属性如下。

- `maxlength`：允许的最大字符数。
- `minlength`：允许的最少字符串。
- `pattern`：输入内容必须匹配的正则表达式。
- `placeholder`：输入为空时显示的示例文本。
- `readonly`：布尔属性，表示该控件的内容是否只读。
- `size`：一个非负整数，表示该输入框显示宽度为多少个字符。
- `spellcheck`：是否启动拼写检查，可能的值为`true`（启用）和`false`（不启用）。

该类型与`<datalist>`标签搭配使用，可以形成下拉列表供用户选择。随着用户不断键入，会缩小显示范围，只显示匹配的备选项。

```html
<input id="myURL" name="myURL" type="url"
       list="defaultURLs">

<datalist id="defaultURLs">
  <option value="https://developer.mozilla.org/" label="MDN Web Docs">
  <option value="http://www.google.com/" label="Google">
  <option value="http://www.microsoft.com/" label="Microsoft">
  <option value="https://www.mozilla.org/" label="Mozilla">
  <option value="http://w3.org/" label="W3C">
</datalist>
```

上面代码中，`<option>`的`label`属性表示文本标签，显示在备选下拉框的右侧，网址显示在左侧。

**（16）tel**

`type="tel"`是一个只能输入电话号码的输入框。由于全世界的电话号码格式都不相同，因此浏览器没有默认的验证模式，大多数时候需要自定义验证。

```html
<input type="tel" id="phone" name="phone"
       pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
       required>

<small>Format: 123-456-7890</small>
```

上面代码定义了一个只能输入10位电话号码的输入框。

该类型的配套属性如下。

- `maxlength`：允许的最大字符数。
- `minlength`：允许的最少字符串。
- `pattern`：输入内容必须匹配的正则表达式。
- `placeholder`：输入为空时显示的示例文本。
- `readonly`：布尔属性，表示该控件的内容是否只读。
- `size`：一个非负整数，表示该输入框显示宽度为多少个字符。

**（17）color**

`type="color"`是一个选择颜色的控件，它的值一律都是`#rrggbb`格式。

```html
<input type="color" id="background" name="background"
           value="#e66465">
```

上面代码在 Chrome 浏览器中，会显示一个`#e66465`的色块。点击色块，就会出现一个拾色器，供用户选择颜色。

如果没有指定`value`属性的初始值，默认值为`#000000`（黑色）。

**（18）date**

`type="date"`是一个只能输入日期的输入框，用户可以输入年月日，但是不能输入时分秒。输入格式是`YYYY-MM-DD`。

```html
<input type="date" id="start" name="start"
       value="2018-07-22"
       min="2018-01-01" max="2018-12-31">
```

上面代码会显示一个输入框，默认日期是2018年7月22日。用户点击以后，会日期选择器，供用户选择新的日期。

该类型有以下配套属性。

- `max`：可以允许的最晚日期，格式为`yyyy-MM-dd`。
- `min`：可以允许的最早日期，格式为`yyyy-MM-dd`。
- `step`：步长值，一个数字，以天为单位。

**（19）time**

`type="time"`是一个只能输入时间的输入框，可以输入时分秒，不能输入年月日。日期格式是24小时制的`hh:mm`，如果包括秒数，格式则是`hh:mm:ss`。日期选择器的形式则随浏览器不同而不同。

```html
<input type="time" id="appt" name="appt"
       min="9:00" max="18:00" required>

<small>营业时间上午9点到下午6点</small>
```

该类型有以下配套属性。

- `max`：允许的最晚时间。
- `min`：允许的最早时间。
- `readonly`：布尔属性，表示用户是否不可以编辑时间。
- `step`：步长值，单位为秒。

```html
<input id="appt" type="time" name="appt" step="2">
```

上面代码中，调节控件的话，时间每次改变的幅度是2秒钟。

**（20）month**

`type="month"`是一个只能输入年份和月份的输入框，格式为`YYYY-MM`。

```html
<input type="month" id="start" name="start"
       min="2018-03" value="2018-05">
```

该类型有以下配套属性。

- `max`：允许的最晚时间，格式为`yyyy-MM`。
- `min`：允许的最早时间，格式为`yyyy-MM`。
- `readonly`：布尔属性，表示用户是否不可以编辑时间。
- `step`：步长值，单位为月。

**（21）week**

`type="week"`是一个输入一年中第几周的输入框。格式为`yyyy-Www`，比如`2018-W18`表示2018年第18周。

```html
<input type="week" name="week" id="camp-week"
       min="2018-W18" max="2018-W26" required>
```

该类型有以下配套属性。

- `max`：允许的最晚时间，格式为`yyyy-Www`。
- `min`：允许的最早时间，格式为`yyyy-Www`。
- `readonly`：布尔属性，表示用户是否不可以编辑时间。
- `step`：步长值，单位为周。

**（22）datetime-local**

`type="datetime-local"`是一个时间输入框，让用户输入年月日和时分，格式为`yyyy-MM-ddThh:mm`。注意，该控件不支持秒。

```html
<input type="datetime-local" id="meeting-time"
       name="meeting-time" value="2018-06-12T19:30"
       min="2018-06-07T00:00" max="2018-06-14T00:00">
```

该类型有以下配套属性。

- `max`：允许的最晚时间，格式为`yyyy-MM-ddThh:mm`。
- `min`：允许的最早时间，格式为`yyyy-MM-ddThh:mm`。
- `step`：步长值，单位为秒，默认值是60。

## `<button>`

`<button>`标签会生成一个可以点击的按钮，没有默认行为，通常需要用`type`属性或脚本指定按钮的功能。

```html
<button>点击</button>
```

上面代码会产生一个按钮，上面的文字就是“点击”。

`<button>`内部不仅放置文字，还可以放置图像，这可以形成图像按钮。

```html
<button name="search" type="submit">
  <img src="search.gif">搜索
</button>
```

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

## `<select>`

`<select>`标签用于生成一个下拉菜单。

```html
<label for="pet-select">宠物：</label>

<select id="pet-select" name="pet-select">
  <option value="">--请选择一项--</option>
  <option value="dog">狗</option>
  <option value="cat">猫</option>
  <option value="others">其他</option>
</select>
```

上面代码中，`<select>`生成一个下拉菜单，菜单标题是“--请选择一项--”，最右侧有一个下拉箭头。点击下拉箭头，会显示三个菜单项，供用户点击选择。

下拉菜单的菜单项由`<option>`标签给出，每个`<option>`代表可以选择的一个值。选中的`<option>`的`value`属性，就是`<select>`控件发送的服务器的值。

`<option>`有一个布尔属性`selected`，一旦设置，就表示该项是默认选中的菜单项。

```html
<select name="choice">
  <option value="first">First Value</option>
  <option value="second" selected>Second Value</option>
  <option value="third">Third Value</option>
</select>
```

上面代码中，第二项`Second Value`是默认选中的。页面加载的时候，会直接显示在下拉菜单上。

`<select>`有如下属性。

- `autofocus`：布尔属性，页面加载时是否自动获得焦点。
- `disabled`：布尔属性，是否禁用当前控件。
- `form`：关联表单的`id`属性。
- `multiple`：布尔属性，是否可以选择多个菜单项。默认情况下，只能选择一项。一旦设置，多数浏览器会显示一个滚动列表框。用户可能需要按住`Shift`或其他功能键，选中多项。
- `name`：控件名。
- `required`：布尔属性，是否为必填控件。
- `size`：设置了`multiple`属性时，页面显示时一次可见的行数，其他行需要滚动查看。

## `<option>`，`<optgroup>`

`<option>`标签用在`<select>`、`<optgroup>`、`<datalist>`里面，表示一个菜单项，参见`<select>`的示例。

它有如下属性。

- `disabled`：布尔属性，是否禁用该项。
- `label`：该项的说明。如果省略，则等于该项的文本内容。
- `selected`：布尔属性，是否为默认值。显然，一组菜单中，只能有一个菜单项设置该属性。
- `value`：该项提交到服务器的值。如果省略，则等于该项的文本内容。

`<optgroup>`表示菜单项的分组，通常用在`<select>`内部。

```html
<label>宠物：
  <select name="pets" multiple size="4">
    <optgroup label="四条腿的宠物">
      <option value="dog">狗</option>
      <option value="cat">猫</option>
    </optgroup>
    <optgroup label="鸟类">
      <option value="parrot">鹦鹉</option>
      <option value="thrush">画眉</option>
    </optgroup>
  </select>
</label>
```

上面代码中，`<select>`是一个下拉菜单，它的内部使用`<optgroup>`将菜单项分成两组。每组有自己的标题，会加粗显示，但是用户无法选中。

它的属性如下。

- `disabled`：布尔设置，是否禁用该组。一旦设置，该组所有的菜单项都不可选。
- `label`：菜单项分组的标题。

## `<datalist>`

`<datalist>`标签是一个容器标签，用于为指定控件提供一组相关数据，通常用于生成输入提示。它的内部使用`<option>`，生成每个菜单项。

```html
<label for="ice-cream-choice">冰淇淋：</label>
<input type="text" list="ice-cream-flavors" id="ice-cream-choice" name="ice-cream-choice">

<datalist id="ice-cream-flavors">
  <option value="巧克力">
  <option value="椰子">
  <option value="薄荷">
  <option value="草莓">
  <option value="香草">
</datalist>
```

上面代码中，`<input>`生成一个文本输入框，用户可以输入文本。`<input>`的`list`属性指定关联的`<datalist>`的`id`属性。`<datalist>`的数据列表用于输入建议，用户点击输入框的时候，会显示一个下拉菜单，里面是建议的输入项。并且还会自动匹配用户已经输入的字符，缩小可选的范围，比如用户输入“香”，则只会显示“香草”这一项。

注意，`<option>`在这里可以不需要闭合标签。

`<option>`标签还可以加入`label`属性，作为说明文字。Chrome 浏览器会将其显示在`value`的下一行。

```html
<datalist id="ide">
  <option value="Brackets" label="by Adobe">
  <option value="Coda" label="by Panic">
</datalist>
```

上面代码的渲染结果是，Chrome 浏览器会在下拉列表显示`value`值（比如`Brackets`），然后在其下方以小字显示`label`值（比如`by Adobe`）。

## `<textarea>`

`<textarea>`是一个块级元素，用来生成多行的文本框。

```html
<textarea id="story" name="story"
          rows="5" cols="33">
这是一个很长的故事。
</textarea>
```

上面代码会生成一个长度为5行，宽度为33个字符的文本框。

该标签有如下属性。

- `autofocus`：布尔属性，是否自动获得焦点。
- `cols`：文本框的宽度，单位为字符，默认值为20。
- `disabled`：布尔属性，是否禁用该控件。
- `form`：关联表单的`id`属性。
- `maxlength`：允许输入的最大字符数。如果未指定此值，用户可以输入无限数量的字符。
- `minlength`：允许输入的最小字符数。
- `name`：控件的名称。
- `placeholder`：输入为空时显示的提示文本。
- `readonly`：布尔属性，控件是否为只读。
- `required`：布尔属性，控件是否为必填。
- `rows`：文本框的高度，单位为行。
- `spellcheck`：是否打开浏览器的拼写检查。可能的值有`true`（打开），`default`（由父元素或网页设置决定），`false`（关闭）。
- `wrap`：输入的文本是否自动换行。可能的值有`hard`（浏览器自动插入换行符`CR + LF`，使得每行不超过控件的宽度），`soft`（输入内容超过宽度时自动换行，但不会加入新的换行符，并且浏览器保证所有换行符都是`CR + LR`，这是默认值），`off`（关闭自动换行，单行长度超过宽度时，会出现水平滚动条）。

## `<output>`

`<output>`标签是一个行内元素，用于显示用户操作的结果。

```html
<input type="number" name="a" value="10"> +
<input type="number" name="b" value="10"> =
<output name="result">20</output>
```

该标签有如下属性。

- `for`：关联控件的`id`属性，表示为该控件的操作结果。
- `form`：关联表单的`id`属性。
- `name`：控件的名称。

## `<progress>`

`<progress>`标签是一个行内元素，表示任务的完成进度。浏览器通常会将显示为进度条。

```html
<progress id="file" max="100" value="70"> 70% </progress>
```

该标签有如下属性。

- `max`：进度条的最大值，应该是一个大于`0`的浮点数。默认值为1。
- `value`：进度条的当前值。它必须是`0`和`max`属性之间的一个有效浮点数。如果省略了`max`属性，该值则必须在`0`和`1`之间。如果省略了`value`属性，则进度条会出现滚动，表明正在进行中，无法知道完成的进度。

## `<meter>`

`<meter>`标签是一个行内元素，表示指示器，用来显示已知范围内的一个值，很适合用于任务的当前进度、磁盘已用空间、充电量等带有比例性质的场合。浏览器通常会将其显示为一个不会滚动的指示条。

```html
<p>烤箱的当前温度是<meter min="200" max="500"
  value="350"> 350 度</meter>。</p>
```

上面代码会显示一个指示条，左侧表示`200`，右侧表示`500`，当前位置停留在`350`。

注意，`<meter>`元素的子元素，正常情况下不会显示。只有在浏览器不支持`<meter>`时才会显示。

该标签有如下属性。

- `min`：范围的下限，必须小于`max`属性。如果省略，则默认为`0`。
- `max`：范围的上限，必须大于`min`属性。如果省略，则默认为`1`。
- `value`：当前值，必须在`min`属性和`max`属性之间。如果省略，则默认为`0`。
- `low`：表示“低端”的上限门槛值，必须大于`min`属性，小于`high`属性和`max`属性。如果省略，则等于`min`属性。
- `high`：表示“高端”的下限门槛值，必须小于`max`属性，大于`low`属性和`min`属性。如果省略，则等于`max`属性。
- `optimum`：指定最佳值，必须在`min`属性和`max`属性之间。它应该与`low`属性和`high`属性一起使用，表示最佳范围。如果`optimum`小于`low`属性，则表示“低端”是最佳范围；如果大于`high`属性，则表示“高端”是最佳范围；如果在`low`和`high`之间，则表示“中间地带”是最佳范围。如果省略，则等于`min`和`max`的中间值。
- `form`：关联表单的`id`属性。

Chrome 浏览器使用三种颜色，表示指示条所处的位置。较好情况时，当前位置为绿色；一般情况时，当前位置为黄色；较差情况时，当前位置为红色。

```html
<meter id="fuel" name="fuel"
       min="0" max="100"
       low="33" high="66" optimum="80"
       value="50">
    at 50/100
</meter>
```

上面代码中，指示条可以分成三段：0 ～ 32，33 ～ 65，66 ～ 100。由于`optimum`属性是`80`，因此`66 ～ 100`是较好情况，`33 ～ 65`是一般情况，`0 ～ 32`是较差情况。浏览器因此会根据`value`属性，将当前位置显示为不同颜色，小于`33`时显示红色，大于`65`时显示绿色，两者之间显示黄色。

## 参考链接

- [HTML Interactive Form Validation](https://webkit.org/blog/7099/html-interactive-form-validation/), by Chris Dumez

