# $html - 网页操作

- 更新时间:2026-10-22 10:55:49

> $html：HTML 文本处理小工具。
> 
> 负责 HTML 特殊字符的转义/还原、删除标签、删除标签属性、简单 XSS 过滤，
> 以及解析腾讯微云分享笔记。适合在抓网页、处理富文本时清洗数据。



```javascript
var out = $html.cleanHtmlTag("<p>你好</p>");
log(out);
```




### escape(html)

> 把字符串里的特殊字符转义成 HTML 实体。
> 
> 逐个字符处理，比如 < 变成 &lt;、& 变成 &amp;，这样字符串里的尖括号就不会被当成标签。

- 参数 : html {string} 要转义的原始字符串
- 返回 : {string} 转义后的字符串


```javascript
// 把带尖括号的文本转义
var html = "<div>123</div>";
var escapeHtml = $html.escape(html);
log(escapeHtml);
```


### unescape(text)

> 把 HTML 实体还原成普通字符（escape 的逆操作）。
> 
> 比如把 &lt; 还原成 <、&nbsp; 还原成空格、&copy; 还原成 ©。

- 参数 : text {string} 含 HTML 实体的字符串
- 返回 : {string} 还原后的普通字符串


```javascript
// 把转义过的文字还原
var result = $html.unescape("a &lt; b &nbsp; c");
log(result);
```


### cleanHtmlTag(text)

> 把文本里所有的 HTML 标签全部删掉，只留纯文字。
> 
> 不管什么标签，只要是 <...> 形式的都去掉。

- 参数 : text {string} 含 HTML 标签的字符串
- 返回 : {string} 去掉标签后的纯文本


```javascript
// 去掉所有标签，得到纯文本
var result = $html.cleanHtmlTag("<p>你好</p><b>世界</b>");
log(result);
```


### removeHtmlTag(text, tagNames)

> 只删掉指定名字的 HTML 标签（标签里的文字内容保留）。
> 
> 第二个参数是要删的标签名数组，比如 ["b","i"] 就去掉粗体斜体标签，里面的字还在。

- 参数 : text {string} 原始 HTML 字符串
- 参数 : tagNames {string[]} 要删除的标签名数组
- 返回 : {string} 处理后的字符串


```javascript
// 去掉 p 和 b 标签，保留文字
var result = $html.removeHtmlTag("<p>你好<b>世界</b></p>", ["p", "b"]);
log(result);
```


### unwrapHtmlTag(text, tagNames)

> 只去掉指定标签的"开始和结束标记"，保留标签包住的内容。
> 
> 和 removeHtmlTag 效果类似：<b>字</b> 变成 字。

- 参数 : text {string} 原始 HTML 字符串
- 参数 : tagNames {string[]} 要拆的标签名数组
- 返回 : {string} 处理后的字符串


```javascript
// 拆掉 b、i 标签但保留内容
var result = $html.unwrapHtmlTag("<b>字</b>", ["b"]);
log(result);
```


### removeHtmlTag(text, withTagContent, tagNames)

> 删除指定标签，可选择是否连同标签里的内容一起删。
> 
> withTagContent 传 true 时，连标签包住的内容一起删；传 false 时只拆标签、留内容。

- 参数 : text {string} 原始 HTML 字符串
- 参数 : withTagContent {boolean} true 连内容一起删，false 只删标签
- 参数 : tagNames {string[]} 要处理的标签名数组
- 返回 : {string} 处理后的字符串


```javascript
// true = 连内容一起删掉
var result = $html.removeHtmlTag("<p>你好</p>", true, ["p"]);
log(result);
```


### removeHtmlAttr(html, attrs)

> 删掉标签里指定名字的属性。
> 
> 比如把所有 onclick="..." 这样的属性去掉，标签本身还在。

- 参数 : html {string} 原始 HTML 字符串
- 参数 : attrs {string[]} 要删除的属性名数组
- 返回 : {string} 处理后的字符串


```javascript
// 去掉 onclick 和 id 属性
var result = $html.removeHtmlAttr("<a onclick=\"f()\" id=\"x\">点</a>", ["onclick", "id"]);
log(result);
```


### removeAllHtmlAttr(html, tagNames)

> 把指定标签身上的所有属性全部清空，只留光秃秃的标签。
> 
> 比如 <div class="a" id="b"> 会变成 <div>。

- 参数 : html {string} 原始 HTML 字符串
- 参数 : tagNames {string[]} 要处理的标签名数组
- 返回 : {string} 处理后的字符串


```javascript
// 把 div 的所有属性清空
var result = $html.removeAllHtmlAttr("<div class=\"a\">字</div>", ["div"]);
log(result);
```


### filter(html)

> 做一个简单的 XSS 过滤：删掉 script、iframe 等危险标签和常见事件属性。
> 
> 处理不可信的 HTML 前先过滤一遍，避免脚本注入。

- 参数 : html {string} 待过滤的 HTML 字符串
- 返回 : {string} 过滤后的安全 HTML


```javascript
// 过滤掉危险标签和属性
var result = $html.filter("<p onclick=\"f()\">你好</p><script>alert(1)</script>");
log(result);
```


### getWeiYunNote(shortLink)

> 解析腾讯微云纯文本分享笔记，返回笔记里的文字内容。
> 
> 用法：在腾讯微云「我的-笔记」建一个纯文本笔记（不要加粗、变色等格式），分享后
> 拿到分享链接最后那段短码，传进来即可。它会联网抓页面并提取笔记正文。

- 参数 : shortLink {string} 微云笔记分享链接的短码部分
- 返回 : {string} 解析出的笔记正文
- 版本 : 1.5.0


```javascript
// 传入分享短链接，拿到笔记文字
var noteContent = $html.getWeiYunNote("bnaMAKsa");
    log(noteContent);
```


