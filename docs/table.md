# 表格标签

表格（table）以行（row）和列（column）的形式展示数据。

## `<table>`，`<caption>`

`<table>`是一个块级容器标签，所有表格内容都要放在这个标签里面。

```html
<table>
  ... ...
</table>
```

`<caption>`总是`<table>`里面的第一个子元素，表示表格的标题。该元素是可选的。

```html
<table>
  <caption>示例表格</caption>
</table>
```

## `<thead>`、`<tbody>`、`<tfoot>`

`<thead>`、`<tbody>`、`<tfoot>`都是块级容器元素，且都是`<table>`的一级子元素，分别表示表头、表体和表尾。

```html
<table>
  <thead>... ...</thead>
  <tbody>... ...</tbody>
  <tfoot>... ...</tfoot>
</table>
```

这三个元素都是可选的。如果使用了`<thead>`，那么`<tbody>`和`<tfoot>`一定在`<thead>`的后面。如果使用了`<tbody>`，那么`<tfoot>`一定在`<tbody>`后面。

大型表格内部可以使用多个`<tbody>`，表示连续的多个部分。

## `<colgroup>`，`<col>`

`<colgroup>`是`<table>`的一级子元素，用来包含一组列的定义。`<col>`是`<colgroup>`的子元素，用来定义表格的一列。

```html
<table>
  <colgroup>
    <col>
    <col>
    <col>
  </colgroup>
</table>
```

上面代码表明表格有3列。

`<col>`不仅是一个单独使用的标签，没有结束标志，而且还是一个空元素，没有子元素。它的主要作用，除了申明表格结构，还可以为表格附加样式。

```html
<table>
  <colgroup>
    <col class="c1">
    <col class="c2">
    <col class="c3">
  </colgroup>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>
```

上面代码中，`<colgroup>`声明表格有三列，每一列有自己的 class，可以使用 CSS 针对每个 class 设定样式，会对整个表格生效。

`<col>`有一个`span`属性，值为正整数，默认为`1`。如果大于1，就表示该列的宽度包含连续的多列。

```html
<table>
  <colgroup>
    <col>
    <col span="2">
    <col>
  </colgroup>
</table>
```

上面代码中，表格的表头定义了3列，实际数据有4列。表头的第2列会连续跨2列。

## `<tr>`

`<tr>`标签表示表格的一行（table row）。如果表格有`<thead>`、`<tbody>`、`<tfoot>`，那么`<tr>`就放在这些容器元素之中，否则直接放在`<table>`的下一级。

```html
<table>
  <tr>...</tr>
  <tr>...</tr>
  <tr>...</tr>
</table>
```

上面代码表示表格共有3行。

## `<th>`，`<td>`

`<th>`和`<td>`都用来定义表格的单元格。其中，`<th>`是标题单元格，`<td>`是数据单元格。

```html
<table>
  <tr>
    <th>学号</th><th>姓名</th>
  </tr>
  <tr>
    <td>001</td><td>张三</td>
  </tr>
  <tr>
    <td>002</td><td>李四</td>
  </tr>
</table>
```

上面代码中，表格一共有三行。第一行是标题行，所以使用`<th>`；第二行和第三行是数据行，所以使用`<td>`。

**（1）`colspan`属性，`rowspan`属性**

单元格会有跨越多行或多列的情况，这要通过`colspan`属性和`rowspan`属性设置，前者表示单元格跨越的栏数，后者表示单元格跨越的行数。它们的值都是一个非负整数，默认为1。

```html
<table>
  <tr>
    <td colspan="2">A</td><td>B</td>
  </tr>
  <tr>
    <td>A</td><td>B</td><td>C</td>
  </tr>
</table>
```

上面代码中，第一行的第一个单元格会跨两列。

**（2）`headers`属性**

如果表格很大，单元格很多，源码里面会看不清，哪个单元格对应哪个表头，这时就可以使用`headers`属性。

```html
<table>
  <tr>
    <th id="no">学号</th><th id="names">姓名</th>
  </tr>
  <tr>
    <td headers="no">001</td><td headers="names">张三</td>
  </tr>
  <tr>
    <td headers="no">002</td><td headers="names">李四</td>
  </tr>
</table>
```

上面代码中，标题栏的`<th>`设置了`id`属性，后面的`<td>`单元格的`headers`属性就对应这些`id`属性的值，因此就能看出来这些单元格对应哪个标题栏。

`headers`属性的值总是对应`<th>`标签的`id`属性的值。由于一个单元格可以对应多个标题栏（跨行的情况），所以`headers`属性可以是一个空格分隔的字符串，对应多个`id`属性的值。

**（3）`scope`属性**

`scope`属性只有`<th>`标签支持，一般不在`<td>`标签使用，表示该`<th>`单元格到底是栏的标题，还是列的标题。

```html
<table>
  <tr>
    <th scope="col">姓名</th>
    <th scope="col">学号</th>
    <th scope="col">性别</th>
  </tr>
  <tr>
    <th scope="row">张三</th>
    <td>001</td>
    <td>男</td>
  </tr>
  <tr>
    <th scope="row">李四</th>
    <td>002</td>
    <td>男</td>
  </tr>
</table>
```

上面代码中，第一行的标题栏都是列标题，所以`<th>`的`scope`属性为`col`，第二行和第三行的第一列是行标题，所以`<th>`标签的`scope`属性为`row`。

`scope`属性可以取下面这些值。

- `row`：该行的所有单元格，都与该标题单元格相关。
- `col`：该列的所有单元格，都与该标题单元格相关。
- `rowgroup`：多行组成的一个行组的所有单元格，都与该标题单元格相关，可以与`rowspan`属性配合使用。
- `colgroup`：多列组成的一个列组的所有单元格，都与该标题单元格相关，可以与`colspan`属性配合使用。
- `auto`：默认值，表示由浏览器自行决定。

下面是一个`colgroup`属性和`rowgroup`属性的例子。

```html
<table>
  <thead>
    <tr>
      <th scope="col">海报名称</th>
      <th scope="col">颜色</th>
      <th colspan="3" scope="colgroup">尺寸</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" scope="rowgroup">Zodiac</th>
      <th scope="row">Full color</th>
      <td>A2</td>
      <td>A3</td>
      <td>A4</td>
    </tr>
    <tr>
      <th scope="row">Black and white</th>
      <td>A1</td>
      <td>A2</td>
      <td>A3</td>
    </tr>
    <tr>
      <th scope="row">Sepia</th>
      <td>A3</td>
      <td>A4</td>
      <td>A5</td>
    </tr>
  </tbody>
</table>
```

上面的例子中，列标题“尺寸”的`scope`属性为`colgroup`，表示这个标题单元格对应多列（本例为3列）；行标题的`scope`属性为`rowgroup`，表示这个标题单元格对应多行（本例为3行）。

渲染结果就是下面的样子。

<table>
  <thead>
    <tr>
      <th scope="col">海报名称</th>
      <th scope="col">颜色</th>
      <th colspan="3" scope="colgroup">尺寸</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" scope="rowgroup">Zodiac</th>
      <th scope="row">Full color</th>
      <td>A2</td>
      <td>A3</td>
      <td>A4</td>
    </tr>
    <tr>
      <th scope="row">Black and white</th>
      <td>A1</td>
      <td>A2</td>
      <td>A3</td>
    </tr>
    <tr>
      <th scope="row">Sepia</th>
      <td>A3</td>
      <td>A4</td>
      <td>A5</td>
    </tr>
  </tbody>
</table>

