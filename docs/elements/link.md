# <link> 元素

```html
<link rel="prefetch" href="/style.css" as="style" />
<link rel="preload" href="/style.css" as="style" />

<link rel="preconnect" href="https://example.com" />
<link rel="dns-prefetch" href="https://example.com" />

<link rel="prerender" href="https://example.com/about.html" />
```

`<link rel="preload">`告诉浏览器尽快下载并缓存资源（如脚本或样式表）。当您在加载页面几秒钟后需要该资源时，它会很有用，并且您希望加快它的速度。

下载后，浏览器不会对资源执行任何操作。脚本未执行，样式表未应用。它只是缓存 - 所以当其他东西需要它时，它立即可用。

```html
<link rel="preload" href="/style.css" as="style" />
```

`href`指向要下载的资源。

`as`可以是您可以在浏览器中下载的任何内容：

- style 对于样式表，
- script 对于脚本，
- font 对于字体，
- fetch资源下载使用fetch()或XMLHttpRequest，
- 其他值 - 请参阅MDN上的完整列表

指定as属性非常重要- 它有助于浏览器确定优先级并正确安排下载。

`<link rel="prefetch">`要求浏览器在后台下载和缓存资源（如脚本或样式表）。下载以低优先级发生，因此它不会干扰更重要的资源。当您知道在后续页面上需要该资源并且您希望提前缓存它时，它会很有用。

下载后，浏览器不会对资源执行任何操作。脚本未执行，样式表未应用。它只是缓存 - 所以当其他东西需要它时，它立即可用。

```html
<link rel="prefetch" href="/style.css" as="style" />
```

href 指向要下载的资源。

as 可以是您可以在浏览器中下载的任何内容：

style 对于样式表，
script 对于脚本，
font 对于字体，
fetch资源下载使用fetch()或XMLHttpRequest，
其他值 - 请参阅MDN上的完整列表
指定as属性非常重要- 它有助于浏览器确定优先级并正确安排下载。

将其用于其他页面的资源。 `<link rel="prefetch">`如果你需要一个不同页面上的资源，并希望预加载它并加速该页面的渲染，将会有所帮助。

该指令不是强制性的。该浏览器并不需要遵循`<link rel="prefetch">`指令。这意味着它可以决定不获取资源 - 例如，如果连接速度很慢。

`<link rel="preconnect">`要求浏览器提前执行与域的连接。当你知道你很快就会从该域下载某些东西时会很有帮助，但是你不知道到底是什么，并且你想加速初始连接。

浏览器在从新的第三方域检索内容时必须建立连接。（第三方域是与您的应用托管的域不同的域。）当站点使用来自Google Fonts的字体，从CDN加载React或从API服务器请求JSON响应时，可能会发生这种情况。

设置新连接通常需要几百毫秒。每个域只需要一次，但仍需要时间。如果您提前设置了连接，则可以节省该时间并更快地从该域加载资源。

```html
<link rel="preconnect" href="https://api.my-app.com" />
```

`<link rel="dns-prefetch">`要求浏览器提前执行域的DNS解析。当您知道很快就会连接到该域时，它会很有用，并且您希望加快初始连接速度。

浏览器在连接到新的第三方域时必须执行DNS解析。（第三方域名是与您的应用托管域名不同的域名。）当您的网站使用Google字体中的字体，从CDN加载React或从您的API服务器请求JSON响应时，可能会发生这种情况。

```html
<link rel="dns-prefetch" href="https://api.my-app.com" />
```

`<link rel="prerender">`要求浏览器加载URL并在不可见的选项卡中呈现它。当用户单击指向该URL的链接时，应立即呈现该页面。当您确定用户将访问下一个特定页面并且您希望更快地呈现它时，它会很有用。

```html
<link rel="prerender" href="https://my-app.com/pricing" />
```

## 参考链接

- [Preload, prefetch and other `<link>` tags](https://3perf.com/blog/link-rels/), Ivan Akulov
