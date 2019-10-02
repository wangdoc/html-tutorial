# 移动设备网页设计

## `<meta>`的 viewport 设置

`<meta>`的 viewport 设置用来控制网页的视觉大小。

```html
<meta name="viewport" content="initial-scale=1">
```

这表示网页初始加载不进行放大或缩小。

下面代码指定网页适配的视口宽度。

```html
<meta name="viewport" content="width=320">
```

下面代码指定网页宽度为设备宽度。

```html
<meta name="viewport" content="width=device-width">
```

下面代码指定用户不能放大网页。

```html
<meta name="viewport" content="maximum-scale=1">
```

适用手机的网页，一般要写成下面这样。

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```



