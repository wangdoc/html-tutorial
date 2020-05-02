# 多媒体标签

除了图像，网页还可以放置视频和音频。

## `<video>`

`<video>`标签是一个块级元素，用于放置视频。如果浏览器支持加载的视频格式，就会显示一个播放器，否则显示`<video>`内部的子元素。

```html
<video src="example.mp4" controls>
  <p>你的浏览器不支持 HTML5 视频，请下载<a href="example.mp4">视频文件</a>。</p>
</video>
```

上面代码中，如果浏览器不支持该种格式的视频，就会显示`<video>`内部的文字提示。

`<video>`有以下属性。

- `src`：视频文件的网址。
- `controls`：播放器是否显示控制栏。该属性是布尔属性，不用赋值，只要写上属性名，就表示打开。如果不想使用浏览器默认的播放器，而想使用自定义播放器，就不要使用该属性。
- `width`：视频播放器的宽度，单位像素。
- `height`：视频播放器的高度，单位像素。
- `autoplay`：视频是否自动播放，该属性为布尔属性。
- `loop`：视频是否循环播放，该属性为布尔属性。
- `muted`：是否默认静音，该属性为布尔属性。
- `poster`：视频播放器的封面图片的 URL。
- `preload`：视频播放之前，是否缓冲视频文件。这个属性仅适合没有设置`autoplay`的情况。它有三个值，分别是`none`（不缓冲）、`metadata`（仅仅缓冲视频文件的元数据）、`auto`（可以缓冲整个文件）。
- `playsinline`：iPhone 的 Safari 浏览器播放视频时，会自动全屏，该属性可以禁止这种行为。该属性为布尔属性。
- `crossorigin`：是否采用跨域的方式加载视频。它可以取两个值，分别是`anonymous`（跨域请求时，不发送用户凭证，主要是 Cookie），`use-credentials`（跨域时发送用户凭证）。
- `currentTime`：指定当前播放位置（双精度浮点数，单位为秒）。如果尚未开始播放，则会从这个属性指定的位置开始播放。
- `duration`：该属性只读，指示时间轴上的持续播放时间（总长度），值为双精度浮点数（单位为秒）。如果是流媒体，没有已知的结束时间，属性值为`+Infinity`。

下面是一个例子。

```html
<video width="400" height="400"
       autoplay loop muted
       poster="poster.png">
</video>
```

上面代码中，视频播放器的大小是 400 x 400，会自动播放和循环播放，并且静音，还带有封面图。这是网站首页背景视频的常见写法。

HTML 标准没有规定浏览器需要支持哪些视频格式，完全由浏览器厂商自己决定。为了避免浏览器不支持视频格式，可以使用`<source>`标签，放置同一个视频的多种格式。

```html
<video controls>
  <source src="example.mp4" type="video/mp4">
  <source src="example.webm" type="video/webm">
  <p>你的浏览器不支持 HTML5 视频，请下载<a href="example.mp4">视频文件</a>。</p>
</video>
```

上面代码中，`<source>`标签的`type`属性的值是视频文件的 MIME 类型，上例指定了两种格式的视频文件：MP4 和 WebM。如果浏览器支持 MP4，就加载 MP4 格式的视频，不再往下执行了。如果不支持 MP4，就检查是否支持 WebM，如果还是不支持，则显示提示。

## `<audio>`

`<audio>`标签是一个块级元素，用于放置音频，用法与`<video>`标签基本一致。

```html
<audio controls>
  <source src="foo.mp3" type="audio/mp3">
  <source src="foo.ogg" type="audio/ogg">
  <p>你的浏览器不支持 HTML5 音频，请直接下载<a href="foo.mp3">音频文件</a>。</p>
</audio>
```

上面代码中，`<audio>`标签内部使用`<source>`标签，指定了两种音频格式：优先使用 MP3 格式，如果浏览器不支持则使用 Ogg 格式。如果浏览器不能播放音频，则提供下载链接。

`<audio>`标签的属性与`<video>`标签类似，参见上一节。

- `autoplay`：是否自动播放，布尔属性。
- `controls`：是否显示播放工具栏，布尔属性。如果不设置，浏览器不显示播放界面，通常用于背景音乐。
- `crossorigin`：是否使用跨域方式请求。
- `loop`：是否循环播放，布尔属性。
- `muted`：是否静音，布尔属性。
- `preload`：音频文件的缓冲设置。
- `src`：音频文件网址。

## `<track>`

`<track>`标签用于指定视频的字幕，格式是 WebVTT （`.vtt`文件），放置在`<video>`标签内部。它是一个单独使用的标签，没有结束标签。

```html
<video controls src="sample.mp4">
   <track label="英文" kind="subtitles" src="subtitles_en.vtt" srclang="en">
   <track label="中文" kind="subtitles" src="subtitles_cn.vtt" srclang="cn" default>
</video>
```

上面代码指定视频文件的英文字幕和中文字幕。

`<track>`标签有以下属性。

- `label`：播放器显示的字幕名称，供用户选择。
- `kind`：字幕的类型，默认是`subtitles`，表示将原始声音成翻译外国文字，比如英文视频提供中文字幕。另一个常见的值是`captions`，表示原始声音的文字描述，通常是视频原始使用的语言，比如英文视频提供英文字幕。
- `src`：vtt 字幕文件的网址。
- `srclang`：字幕的语言，必须是有效的语言代码。
- `default`：是否默认打开，布尔属性。

## `<source>`

`<source>`标签用于`<picture>`、`<video>`、`<audio>`的内部，用于指定一项外部资源。单标签是单独使用的，没有结束标签。

它有如下属性，具体示例请参见相应的容器标签。

- `type`：指定外部资源的 MIME 类型。
- `src`：指定源文件，用于`<video>`和`<audio>`。
- `srcset`：指定不同条件下加载的图像文件，用于`<picture>`。
- `media`：指定媒体查询表达式，用于`<picture>`。
- `sizes`：指定不同设备的显示大小，用于`<picture>`，必须跟`srcset`搭配使用。

## `<embed>`

`<embed>`标签用于嵌入外部内容，这个外部内容通常由浏览器插件负责控制。由于浏览器的默认插件都不一致，很可能不是所有浏览器的用户都能访问这部分内容，建议谨慎使用。

下面是嵌入视频播放器的例子。

```html
<embed type="video/webm"
       src="/media/examples/flower.mp4"
       width="250"
       height="200">
```

上面代码嵌入的视频，将由浏览器插件负责控制。如果浏览器没有安装 MP4 插件，视频就无法播放。

`<embed>`标签具有如下的通用属性。

- `height`：显示高度，单位为像素，不允许百分比。
- `width`：显示宽度，单位为像素，不允许百分比。
- `src`：嵌入的资源的 URL。
- `type`：嵌入资源的 MIME 类型。

浏览器通过`type`属性得到嵌入资源的 MIME 类型，一旦该种类型已经被某个插件注册了，就会启动该插件，负责处理嵌入的资源。

下面是 QuickTime 插件播放 MOV 视频文件的例子。

```html
<embed type="video/quicktime" src="movie.mov" width="640" height="480">
```

下面是启动 Flash 插件的例子。

```html
<embed src="whoosh.swf" quality="medium"
       bgcolor="#ffffff" width="550" height="400"
       name="whoosh" align="middle" allowScriptAccess="sameDomain"
       allowFullScreen="false" type="application/x-shockwave-flash"
       pluginspage="http://www.macromedia.com/go/getflashplayer">
```

上面代码中，如果浏览器没有安装 Flash 插件，就会提示去`pluginspage`属性指定的网址下载。

## `<object>`，`<param>`

`<object>`标签作用跟`<embed>`相似，也是插入外部资源，由浏览器插件处理。它可以视为`<embed>`的替代品，有标准化行为，只限于插入少数几种通用资源，没有历史遗留问题，因此更推荐使用。

下面是插入 PDF 文件的例子。

```html
<object type="application/pdf"
    data="/media/examples/In-CC0.pdf"
    width="250"
    height="200">
</object>
```

上面代码中，如果浏览器安装了 PDF 插件，就会在网页显示 PDF 浏览窗口。

`<object>`具有如下的通用属性。

- `data`：嵌入的资源的 URL。
- `form`：当前网页中相关联表单的`id`属性（如果有的话）。
- `height`：资源的显示高度，单位为像素，不能使用百分比。
- `width`：资源的显示宽度，单位为像素，不能使用百分比。
- `type`：资源的 MIME 类型。
- `typemustmatch`：布尔属性，表示`data`属性与`type`属性是否必须匹配。

下面是插入 Flash 影片的例子。

```html
<object data="movie.swf"
  type="application/x-shockwave-flash"></object>
```

`<object>`标签是一个容器元素，内部可以使用`<param>`标签，给出插件所需要的运行参数。

```html
<object data="movie.swf" type="application/x-shockwave-flash">
  <param name="foo" value="bar">
</object>
```

