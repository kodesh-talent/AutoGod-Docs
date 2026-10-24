# $ - 桥梁对象

- 更新时间:2026-10-22 10:58:43

> 连接应用网页控件与 Rhino 脚本的桥梁对象。
> 
> 控件默认把本对象注入网页并命名为 $；通过 bridge 属性可以更换名字。这里的示例应放在该控件的网页中运行。
> Rhino 脚本先通过网页控件 addFunc 注册回调，网页再使用 $.call 调用。直接在普通浏览器或 Rhino 全局中输入 $.call 不会自动得到此桥梁。
> 函数参数按字符串传递，回调最多接收十个业务参数；网页未提供的位置由桥梁填为 null。



```javascript
$.log("网页桥梁已可用"); // 在控件加载的网页中验证默认桥梁。
```




### call(funcName)

> 网页调用已注册的脚本函数，传入 0 个业务参数。
> 
> funcName 是注册名称，不计入业务参数数量；所有输入类型均为 String（字符串），返回类型也为 String。
> 网页端的 $ 默认是此桥梁；Rhino 脚本端通过网页控件 addFunc 注册回调，这两个位置的代码不能混在同一个执行环境。
> 未注册该名称时返回 null；已注册时直接返回回调结果。funcName 不应为 null，桥梁不会捕获回调抛出的异常。
> 回调接口 WebFuncCallBack 总共有十个参数，本重载填写前 0 项，其余传 null。
> 请主动传字符串；要传对象，可先 JSON.stringify，在回调中再 JSON.parse。数字或布尔值也建议先 String(...)，不要依赖隐式转换。
> 第一段在 Rhino 脚本中执行：

- 参数 : funcName {String} 与脚本注册名称一致的非空引用字符串
- 返回 : {String} 回调返回的文字；找不到注册函数或回调返回空值时为 null


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb"/></ui>'); // 创建网页控件。
ui.show(); // 显示界面。
var web = ui.id("mWeb"); // 根据编号取出控件。
web.addFunc("sample0", function() { // 注册回调。
    return "received"; // 返回文字给发起调用的网页。
});
```

```javascript
var reply = $.call("sample0"); // 按顺序传入字符串。
if (reply != null) {
    $.log(String(reply)); // 网页通过桥梁打印返回文字。
} else {
    $.log("未得到返回文字，请检查注册名称或回调返回值");
}
```


### call(funcName, args)

> 网页调用已注册的脚本函数，传入 1 个业务参数。
> 
> funcName 是注册名称，不计入业务参数数量；所有输入类型均为 String（字符串），返回类型也为 String。
> 网页端的 $ 默认是此桥梁；Rhino 脚本端通过网页控件 addFunc 注册回调，这两个位置的代码不能混在同一个执行环境。
> 未注册该名称时返回 null；已注册时直接返回回调结果。funcName 不应为 null，桥梁不会捕获回调抛出的异常。
> 回调接口 WebFuncCallBack 总共有十个参数，本重载填写前 1 项，其余传 null。
> 请主动传字符串；要传对象，可先 JSON.stringify，在回调中再 JSON.parse。数字或布尔值也建议先 String(...)，不要依赖隐式转换。
> 第一段在 Rhino 脚本中执行：

- 参数 : funcName {String} 与脚本注册名称一致的非空引用字符串
- 参数 : args {String} 第 1 个业务参数，原样传给回调
- 返回 : {String} 回调返回的文字；找不到注册函数或回调返回空值时为 null


```javascript
var ui = $ui.layout('<ui><statusbar/><webview id="mWeb"/></ui>'); // 创建网页控件。
ui.show(); // 显示界面。
var web = ui.id("mWeb"); // 根据编号取出控件。
web.addFunc("sample1", function(arg1) { // 注册回调。
    log(String(arg1)); // 查看第 1 个业务参数。
    return "received"; // 返回文字给发起调用的网页。
});
```

```javascript
var reply = $.call("sample1", "value1"); // 按顺序传入字符串。
if (reply != null) {
    $.log(String(reply)); // 网页通过桥梁打印返回文字。
} else {
    $.log("未得到返回文字，请检查注册名称或回调返回值");
}
```


### log(log)

> 把网页中的文字写入应用日志。
> 
> 下面代码在应用网页控件加载的网页中执行，$ 为默认桥梁名称，不是 Rhino 脚本中的独立全局工具。
> 如果控件用 bridge 属性改过桥梁名称，网页里也需要改用对应名称。
> 输入为 String（字符串），返回 void，没有返回值。复杂对象请先 JSON.stringify 转成文字。

- 参数 : log {String} 要写入日志的文字
- 返回 : {void} 无返回值


```javascript
$.log("网页按钮被点击了"); // 在应用日志中记录调试信息。
```


### toast(msg)

> 从网页显示短暂的文字提示。
> 
> 下面代码在应用网页控件加载的网页中执行，$ 为默认桥梁名称，不是 Rhino 脚本中的独立全局工具。
> 如果控件用 bridge 属性改过桥梁名称，网页里也需要改用对应名称。
> 输入为 String（字符串），返回 void，没有返回值；不能通过返回值判断用户是否看到了提示。

- 参数 : msg {String} 要显示的提示文字
- 返回 : {void} 无返回值


```javascript
$.toast("操作已完成"); // 显示短暂提示，不等待用户输入。
```


### alert(msg)

> 从网页显示文字提示对话框。
> 
> 下面代码在应用网页控件加载的网页中执行，$ 为默认桥梁名称，不是 Rhino 脚本中的独立全局工具。
> 如果控件用 bridge 属性改过桥梁名称，网页里也需要改用对应名称。
> 输入一个 String，作为提示文字。
> 返回 void，没有返回值；该接口不是确认选择接口，不能据此决定是否删除数据。

- 参数 : msg {String} 要显示的提示文字
- 返回 : {void} 无返回值


```javascript
$.alert("请检查填写的信息"); // 仅显示提示，不会返回用户选择。
```


### alert(title, msg)

> 从网页显示文字提示对话框。
> 
> 下面代码在应用网页控件加载的网页中执行，$ 为默认桥梁名称，不是 Rhino 脚本中的独立全局工具。
> 如果控件用 bridge 属性改过桥梁名称，网页里也需要改用对应名称。
> 输入两个 String，依次为标题和正文。
> 返回 void，没有返回值；该接口不是确认选择接口，不能据此决定是否删除数据。

- 参数 : title {String} 对话框标题
- 参数 : msg {String} 要显示的提示文字
- 返回 : {void} 无返回值


```javascript
$.alert("提示", "请检查填写的信息"); // 仅显示提示，不会返回用户选择。
```


### getClip()

> 从网页读取剪贴板第一项的文字。
> 
> 下面代码在应用网页控件加载的网页中执行，$ 为默认桥梁名称，不是 Rhino 脚本中的独立全局工具。
> 如果控件用 bridge 属性改过桥梁名称，网页里也需要改用对应名称。
> 没有输入参数；返回 String（字符串）。没有剪贴板数据或没有条目时返回 null。
> 当前工具直接读取第一项的文本；如果第一项不含文本，读取过程可能抛出异常，不能假设所有剪贴板内容都可转换。

- 返回 : {String} 剪贴板第一项文字，可能为 null


```javascript
try {
    var text = $.getClip(); // 尝试读取第一项文字。
    if (text != null) {
        $.log("已读取剪贴板文字，长度为：" + String(text).length); // 只输出长度。
    } else {
        $.log("没有可读取的剪贴板条目");
    }
} catch (err) {
    $.log("剪贴板读取未成功"); // 非文本条目等情况需要另行处理。
}
```


### setClip(text)

> 把文字交给剪贴板写入工具。
> 
> 下面代码在应用网页控件加载的网页中执行，$ 为默认桥梁名称，不是 Rhino 脚本中的独立全局工具。
> 如果控件用 bridge 属性改过桥梁名称，网页里也需要改用对应名称。
> Java 声明的输入类型为 CharSequence（字符序列），返回 void，没有返回值。参数为 null 时直接结束，不清空剪贴板。
> 非空输入会调用 toString 后写入剪贴板。本例表达传入文本的用法，网页到 CharSequence 的转换需要在目标 WebView 上验证。

- 参数 : text {CharSequence} 待写入的字符序列；null 时不操作
- 返回 : {void} 无返回值


```javascript
$.setClip("准备复制的文字"); // 尝试将文字交给桥梁。
// 此方法不返回是否写入成功；可在目标设备上粘贴检查。
```


