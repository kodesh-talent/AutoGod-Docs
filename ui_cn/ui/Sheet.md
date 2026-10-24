# Sheet - 底部弹窗

- 更新时间:2026-10-22 10:58:38

> 底部弹窗




### 解析布局(xml内容或路径)

> 解析底部弹窗的布局。每个弹窗只解析一次；重复调用会保留首次解析的布局。

- 参数 : xml内容或路径 {string} xml内容或者xml路径
- 返回 : {底部弹窗} 返回自己
- 版本 : 1.5.5


```}
var page = $ui.layout("main.xml");
var sheet = $ui.sheet(page.activity());
sheet.解析布局("sheet.xml");
```


### 获得视图()

> 获取弹窗布局的根 Android 视图。尚未解析布局时返回 null。

- 返回 : 弹窗布局的根视图；尚未解析布局时为 null
- 版本 : 1.5.8


```}
var page = $ui.layout("main.xml");
var sheet = $ui.sheet(page.activity());
sheet.解析布局("sheet.xml");
var rootView = sheet.获得视图();
```


### 找控件(标识)

> 按布局中的标识查找弹窗内的控件。请先调用 {@link #解析布局(String)} 解析布局。

- 参数 : 标识 {string} 控件标识
- 返回 : 找到的控件；没有匹配的标识时返回 null
- 版本 : 1.5.8


```}
var page = $ui.layout("main.xml");
var sheet = $ui.sheet(page.activity());
sheet.解析布局("sheet.xml");
var title = sheet.找控件("title");
```


### 显示()

> 显示底部弹窗。请先解析布局；未解析时会记录警告并跳过显示。

- 返回 : 当前底部弹窗对象，可继续链式调用
- 版本 : 1.5.8


```}
var page = $ui.layout("main.xml");
var sheet = $ui.sheet(page.activity());
sheet.解析布局("sheet.xml");
sheet.显示();
```


### 关闭()

> 关闭当前底部弹窗。弹窗尚未显示时会记录警告并跳过关闭。

- 返回 : 当前底部弹窗对象，可继续链式调用
- 版本 : 1.5.8


```}
var page = $ui.layout("main.xml");
var sheet = $ui.sheet(page.activity());
sheet.解析布局("sheet.xml");
sheet.显示();
sheet.关闭();
```


