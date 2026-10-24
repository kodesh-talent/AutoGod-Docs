# 网页

- 更新时间:2026-10-22 10:58:43

> 网页-webview
> 
> 你可以用vant,vue,layui,element-ui等框架编写html界面，在这个控件中加载这个界面，之后就是处理一些交互函数了





<div style="width: 100%; position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe 
    src="//player.bilibili.com/player.html?isOutside=true&aid=116242836888247&bvid=BV1HRwDzvEjs&cid=36758423061&p=1" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;"
    scrolling="no" 
    frameborder="no" 
    allowfullscreen="true">
  </iframe>
</div>

强大的网页组件，可以展示华丽的html页面。


## 一、常用属性


### 桥梁 - 桥梁对象名称

> 设置桥梁对象名称


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态条 />
    <网页 桥梁="bridge" />
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


### 路径 - 网页路径

> 设置网页路径


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
// 示例用到的本地资源需要提前准备，请把文件路径改为项目中的实际路径。
var 布局内容 = `
<界面>
    <状态条 />
    <网页 路径="layout.html" />
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


### 链接 - 网页链接

> 设置网页链接


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
// 网络内容需要可用的地址和网络连接；请按实际情况替换示例地址。
var 布局内容 = `
<界面>
    <状态条 />
    <网页 链接="https://auto-god.netlify.app/" />
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


### 内边距 - 内边距

> 设置内边距


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态条 />
    <网页 内边距="0,0,0,0" />
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


### 背景颜色 - 背景颜色

> 设置背景颜色


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态条 />
    <网页 背景颜色="red" />
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


### 背景图片 - 背景图片

> 设置背景图片


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
// 示例用到的本地资源需要提前准备，请把文件路径改为项目中的实际路径。
var 布局内容 = `
<界面>
    <状态条 />
    <网页 背景图片="res/bg.png" />
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


## 二、常用函数


### onLoaded(onLoad)

> 监听网页“整页加载完成”这一刻，立刻回调你传进来的函数（无参数）。
> 
> 一般在这里面注册网页要调用的函数（addFunc），因为注册太早网页还没准备好。

- 参数 : onLoad {function} 网页加载完成时回调，无参数


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" url="https://example.com"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.onLoaded(function() {
    log("网页加载完了");
    wv.addFunc("onBtn", function() {
        log("网页里按钮被点了");
        return "";
    });
});
```


### clear()

> 清空这个网页控件的缓存、历史记录和表单数据（让它像刚打开一样干净）。


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" url="https://example.com"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.clear(); //清掉缓存和历史
```


### loadUrl(url)

> 让网页控件打开一个新的网址（会自动补 http:// 开头）。

- 参数 : url {String} 要打开的网址


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.loadUrl("https://www.baidu.com"); //打开百度
```


### loadHtml(html)

> 直接用一段 HTML 字符串当网页内容显示出来（不用先写文件）。

- 参数 : html {String} 要显示的 HTML 字符串


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
//用 + 拼接一段简单网页
var html = '<html><body><h1>你好</h1></body></html>';
wv.loadHtml(html); //直接显示这段网页
```


### loadFile(path)

> 让网页控件加载项目里的一个本地 HTML 文件。

- 参数 : path {String} 本地 HTML 文件路径


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.loadFile("index.html"); //加载项目里这个网页文件
```


### callJs(funcName, callBack)

> 在脚本端去调用网页里写好的一个无参 JS 函数，并能收到它 return 的结果。
> 
> 网页里必须已经定义好这个函数名；网页没加载完时调用会失败。

- 参数 : funcName {String} 网页里已定义的无参 JS 函数名
- 参数 : callBack {function} 收到函数返回值（字符串）的回调


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
//网页里定义了 function mFunc(){return 123;}
wv.callJs("mFunc", function(returnValue) {
    log("网页返回:" + returnValue);
});
```


### callJs(funcName)

> 在脚本端去调用网页里写好的一个无参 JS 函数（不关心它的返回值）。

- 参数 : funcName {String} 网页里已定义的无参 JS 函数名


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJs("mFunc"); //网页里定义了 function mFunc(){...}
```


### callJsInt(funcName, param, callBack)

> 在脚本端调用网页里的一个 JS 函数，并传一个整数进去，还能收到返回值。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {Number} 要传进去的整数
- 参数 : callBack {function} 收到返回值（字符串）的回调


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
//网页里定义了 function setFontSize(n){...}
wv.callJsInt("setFontSize", 22, function(returnValue) {
    log("网页返回:" + returnValue);
});
```


### callJsInt(funcName, param)

> 在脚本端调用网页里的一个 JS 函数，传一个整数进去（不关心返回值）。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {Number} 要传进去的整数


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsInt("setFontSize", 22); //网页里定义了 function setFontSize(n){...}
```


### callJsLong(funcName, param, callBack)

> 在脚本端调用网页里的一个 JS 函数，并传一个很大的整数（长整数）进去，能收到返回值。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {Number} 要传进去的长整数
- 参数 : callBack {function} 收到返回值（字符串）的回调


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsLong("setLength", 546894564564849, function(returnValue) {
    log("网页返回:" + returnValue);
});
```


### callJsLong(funcName, param)

> 在脚本端调用网页里的一个 JS 函数，传一个很大的整数（长整数）进去（不关心返回值）。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {Number} 要传进去的长整数


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsLong("setLength", 546894564564849);
```


### callJsDouble(funcName, param, callBack)

> 在脚本端调用网页里的一个 JS 函数，并传一个带小数的数字进去，能收到返回值。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {Number} 要传进去的小数
- 参数 : callBack {function} 收到返回值（字符串）的回调


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsDouble("setVal", 3.1415926, function(returnValue) {
    log("网页返回:" + returnValue);
});
```


### callJsDouble(funcName, param)

> 在脚本端调用网页里的一个 JS 函数，传一个带小数的数字进去（不关心返回值）。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {Number} 要传进去的小数


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsDouble("setVal", 3.1415926);
```


### callJsFloat(funcName, param, callBack)

> 在脚本端调用网页里的一个 JS 函数，并传一个小数进去，能收到返回值。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {Number} 要传进去的小数
- 参数 : callBack {function} 收到返回值（字符串）的回调


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsFloat("setVal", 3.14, function(returnValue) {
    log("网页返回:" + returnValue);
});
```


### callJsFloat(funcName, param)

> 在脚本端调用网页里的一个 JS 函数，传一个小数进去（不关心返回值）。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {Number} 要传进去的小数


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsFloat("setVal", 3.14);
```


### callJsChar(funcName, param, callBack)

> 在脚本端调用网页里的一个 JS 函数，并传一个单字符进去，能收到返回值。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {String} 要传进去的单字符
- 参数 : callBack {function} 收到返回值（字符串）的回调


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsChar("setChar", "A", function(returnValue) {
    log("网页返回:" + returnValue);
});
```


### callJsChar(funcName, param)

> 在脚本端调用网页里的一个 JS 函数，传一个单字符进去（不关心返回值）。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {String} 要传进去的单字符


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsChar("setChar", "A");
```


### callJsBool(funcName, param, callBack)

> 在脚本端调用网页里的一个 JS 函数，并传一个真/假值（true/false）进去，能收到返回值。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {Boolean} 要传进去的 true 或 false
- 参数 : callBack {function} 收到返回值（字符串）的回调


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsBool("setEnable", true, function(returnValue) {
    log("网页返回:" + returnValue);
});
```


### callJsBool(funcName, param)

> 在脚本端调用网页里的一个 JS 函数，传一个真/假值进去（不关心返回值）。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {Boolean} 要传进去的 true 或 false


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsBool("setEnable", true);
```


### callJsStr(funcName, param, callBack)

> 在脚本端调用网页里的一个 JS 函数，并传一段长文本进去，能收到返回值。
> 
> 长文本会先做 URL 编码，网页里收到后要用 decodeURIComponent 解码才能还原原文。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {String} 要传进去的长文本
- 参数 : callBack {function} 收到返回值（字符串）的回调


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsStr("setCode", "一大段文字", function(returnValue) {
    log("网页返回:" + returnValue);
});
//网页里这样接：
// function setCode(str){
//     var code = decodeURIComponent(str);
//     $.alert("代码", code);
// }
```


### callJsStr(funcName, param)

> 在脚本端调用网页里的一个 JS 函数，传一段长文本进去（不关心返回值）。
> 
> 长文本会先做 URL 编码，网页里收到后要用 decodeURIComponent 解码才能还原原文。

- 参数 : funcName {String} 网页里的 JS 函数名
- 参数 : param {String} 要传进去的长文本


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max" path="index.html"/></ui>');
ui.show(); //把界面显示出来
var wv = ui.id("mWeb"); //根据 id 拿到这个网页控件
wv.callJsStr("setCode", "一大段文字");
//网页里这样接：
// function setCode(str){
//     var code = decodeURIComponent(str);
//     $.alert("代码", code);
// }
```


### addFunc(funcName, callback)

> 注册一个供当前网页调用的脚本函数。
> 
> funcName 为 String（注册名称），callback 为 WebFuncCallBack 回调接口；Rhino 脚本可传 function 实现。返回 void，无返回值。
> 名称和回调都不能为 null；再次注册同名函数会替换原回调。注册只保存回调，不会立即执行它。
> 网页通过默认桥梁 $.call("名称", ...) 调用，最多传十个字符串参数；不足的位置由桥梁填 null，回调返回 String 文字给网页。
> 需要传对象时，网页先 JSON.stringify，脚本回调再 JSON.parse。不要把网页代码与 Rhino 代码放在同一执行环境。
> 可以先注册再加载自己的网页，确保网页调用前名称已经存在；并不要求只能在 onLoaded 中注册。

- 参数 : funcName {String} 网页调用时使用的名称，不能为 null
- 参数 : callback {WebFuncCallBack} 接收最多十个 String 参数并返回 String 的回调，不能为 null
- 返回 : {void} 无返回值


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb" w="max"/></ui>'); // 创建界面。
ui.show(); // 显示控件。
var web = ui.id("mWeb"); // 取得网页控件。
web.addFunc("greet", function(name) { // 注册一个字符串参数的回调。
    if (name == null) { // 网页没有传名字时使用默认值。
        name = "访客";
    }
    return "你好，" + String(name); // 返回文字给网页。
});
// 网页按钮点击时调用桥梁，并通过桥梁显示返回文字。
var html = '<html><body><button onclick="$.toast($.call(\'greet\', \'小明\'))">打招呼</button></body></html>';
web.loadHtml(html); // 注册完成后再加载这段网页。
```


