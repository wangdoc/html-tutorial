# 基本语法

HTML是大小写不敏感的。`<a>`和`<A>`是同一个标签，`onclick`与`onClick`是同一个属性。

## doctype

HTML5 的`doctype`非常简单，只要声明`html`即可。

```html
<!doctype html>
```

## 语义元素

HTML5 引入一系列带有语义的区块，不必再使用`<div>`了。

- `<main>`：主区块
- `<aside>`：副内容
- `<nav>`：导航区块
- `<article>`：内容区块，网页中可以有多个`<article>`，一个`<article>`也可以包含多个`<section>`
- `<section>`：结构区块，一个`<section>`可以包含多个`<article>`
- `<header>`：头部区块
- `<footer>`：尾部区块
- `<figure>`：图片区块
- `<figcaption>`：图片标题区块


