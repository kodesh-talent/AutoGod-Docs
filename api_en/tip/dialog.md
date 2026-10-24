# $dialog - M3对话框

- 更新时间:2026-10-22 10:55:52

> Material 风格（M3）提示框（对话框）。
> 
> 用法和 $alert 几乎一模一样，区别只是外观用的是新版 Material Design 样式，
> 看起来更现代。同样是链式：先 create() 创建，再一路 .标题(...)、.内容(...)、
> .按钮3(...) 把内容设好，最后 .显示() 弹出来。



```javascript
var dlg = $dialog.create();          //创建一个 M3 风格对话框
dlg.标题("确认");
dlg.内容("确定要继续吗？");
dlg.按钮3("确定", function() {
    log("点了确定");
});
dlg.显示();
```




### create()

> 创建一个新的 M3 对话框对象。

- 返回 : {AgDialog} 新建的对话框对象，可继续链式设置


```javascript
var dlg = $dialog.create();  //创建一个对话框
```


### title(title)

> 设置对话框顶部的标题文字。
> 
> 传空字符串则不设置标题。返回对话框自己，可链式继续设置。

- 参数 : title {String} 标题文字
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.title("温馨提示");   //设置对话框标题
```


### isShowing()

> 检查这个对话框现在是否正显示在屏幕上。

- 返回 : {boolean} 正在显示返回 true；没显示或已关闭返回 false


```javascript
var dlg = $dialog.create();
if (dlg.isShowing()) {
    log("对话框正在显示");
}
```


### msg(msg)

> 设置对话框正文的内容文字。
> 
> 传空则不显示。返回对话框自己，可链式继续设置。

- 参数 : msg {String} 正文文字
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.msg("这里是要告诉用户的内容");   //设置正文
```


### cancelable(cancelable)

> 设置用户能不能按返回键、或点弹窗外的空白处来关掉它。
> 
> 传 true 允许取消；传 false 只能靠点按钮才能关掉。返回对话框自己，可链式继续设置。

- 参数 : cancelable {boolean} true 允许取消，false 不允许取消
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.cancelable(false);   //设为不可随便取消，必须点按钮
```


### icon(icon)

> 设置对话框标题左边的小图标。
> 
> 传一个图标名字（图标库里有的）或一张图片的路径；找不到就不设置。
> 返回对话框自己，可链式继续设置。

- 参数 : icon {String} 图标名或图片文件路径
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.icon("info");   //用图标库里名为 info 的图标
```


### view(view)

> 用一个自定义视图（View）作为对话框的内容。
> 
> 先用 $ui.layout 加载一个布局拿到 View，再传给它。传进去后原来的正文会被清空。
> 返回对话框自己，可链式继续设置。

- 参数 : view {View} 要放进对话框的自定义视图
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var ui = $ui.layout("main.xml");   //解析一个布局
var view = ui.getView();          //拿到根视图
var dlg = $dialog.create();
dlg.view(view);                   //把自定义视图放进对话框
```


### view(view)

> 用一个 XView 控件作为对话框的内容（重载）。
> 
> 直接传一个用 $ui.id(...) 取到的 XView 控件。传 null 会打印“视图(view)为空”。
> 返回对话框自己，可链式继续设置。

- 参数 : view {XView} 要放进对话框的 XView 控件
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var ui = $ui.layout("main.xml");
var view = ui.id("myView");       //按 id 取到一个 XView 控件
var dlg = $dialog.create();
dlg.view(view);
```


### but1(text)

> 设置第一个按钮（最左边那个），只显示文字，点了就关闭、不做事。
> 
> 返回对话框自己，可链式继续设置。

- 参数 : text {CharSequence} 按钮上显示的文字
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.but1("取消");   //设置第一个按钮的文字
```


### but1(text, callback)

> 设置第一个按钮（最左边那个），并指定被点击时要做的事（带回调的重载）。
> 
> 第二个参数传一个函数，用户点了这个按钮就会在后台线程执行它，收到
> (对话框, 按钮编号) 两个参数。

- 参数 : text {CharSequence} 按钮上显示的文字
- 参数 : callback {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.but1("取消", function(dialog, which) {
    log("我被点击了");
});
```


### but2(text)

> 设置第二个按钮（中间那个），只显示文字，点了就关闭、不做事。
> 
> 返回对话框自己，可链式继续设置。

- 参数 : text {CharSequence} 按钮上显示的文字
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.but2("稍后提醒");
```


### but2(text, callback)

> 设置第二个按钮（中间那个），并指定被点击时要做的事（带回调的重载）。
> 
> 第二个参数传一个函数，用户点了这个按钮就会在后台线程执行它，收到
> (对话框, 按钮编号) 两个参数。

- 参数 : text {CharSequence} 按钮上显示的文字
- 参数 : callback {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.but2("稍后提醒", function(dialog, which) {
    log("我被点击了");
});
```


### but3(text)

> 设置第三个按钮（最右边那个，通常是“确定”），只显示文字，点了就关闭、不做事。
> 
> 返回对话框自己，可链式继续设置。

- 参数 : text {CharSequence} 按钮上显示的文字
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.but3("确定");
```


### but3(text, callback)

> 设置第三个按钮（最右边那个，通常是“确定”），并指定被点击时要做的事（带回调的重载）。
> 
> 第二个参数传一个函数，用户点了这个按钮就会在后台线程执行它，收到
> (对话框, 按钮编号) 两个参数。

- 参数 : text {CharSequence} 按钮上显示的文字
- 参数 : callback {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.but3("确定", function(dialog, which) {
    log("我被点击了");
});
```


### items(items, callback)

> 把对话框内容变成一组可点的列表选项（普通列表，没有勾选标记）。
> 
> 第一个参数传字符串数组，每一项就是列表里的一行；点某一行就执行第二个参数的函数，
> which 是被点那行的序号（从 0 开始）。选项、单选、多选三种互斥，同一次只能用一种。

- 参数 : items {String[]} 选项文字组成的数组
- 参数 : callback {Function} 点选项后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var 菜单 = ["安卓", "苹果", "鸿蒙"];
var dlg = $dialog.create();
dlg.items(菜单, function(dialog, which) {
    log("你选了第 " + which + " 项");
});
```


### oneItems(items, checkedItem, callback)

> 把对话框内容变成一组单选选项（每行前面带圆圈，只能选一个）。
> 
> 第二个参数是默认选中项的序号（从 0 开始，-1 都不选）；点某行执行第三个参数的函数，
> which 就是被选那行的序号。

- 参数 : items {String[]} 选项文字组成的数组
- 参数 : checkedItem {int} 默认选中项的序号（从 0 开始，-1 都不选）
- 参数 : callback {Function} 点选项后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var 字号 = ["小", "中", "大"];
var dlg = $dialog.create();
dlg.oneItems(字号, 1, function(dialog, which) {
    log("选了第 " + which + " 项");
});
```


### moreItems(items, callback)

> 把对话框内容变成一组多选选项（每行前面带方框，可同时勾多个，默认全不勾）。
> 
> 点某行执行第二个参数的函数，收到 (对话框, 行号, 现在是否勾上)。

- 参数 : items {String[]} 选项文字组成的数组
- 参数 : callback {Function} 勾选变化时执行的函数，形如 function(dialog, which, isChecked) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var 权限 = ["定位", "存储", "相机"];
var dlg = $dialog.create();
dlg.moreItems(权限, function(dialog, which, isChecked) {
    log("第 " + which + " 项现在是：" + isChecked);
});
```


### moreItems(items, checkedItems, callback)

> 把对话框内容变成一组多选选项，并指定每一项默认勾不勾（重载）。
> 
> 第二个参数是布尔数组，长度和选项数组一致，true 表示那一项默认就勾上。

- 参数 : items {String[]} 选项文字组成的数组
- 参数 : checkedItems {boolean[]} 每一项的初始勾选状态，长度和选项数组一致
- 参数 : callback {Function} 勾选变化时执行的函数，形如 function(dialog, which, isChecked) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var 权限 = ["定位", "存储", "相机"];
var 默认勾 = [true, false, false];
var dlg = $dialog.create();
dlg.moreItems(权限, 默认勾, function(dialog, which, isChecked) {
    log("第 " + which + " 项现在是：" + isChecked);
});
```


### show()

> 把设置好的对话框真正显示到屏幕上。
> 
> 前面的设置都只是“先准备着”，必须调 show() 才会弹出来。没授予悬浮窗权限时会提示。

- 返回 : {AlertDialog} 系统对话框对象本身，一般不用接


```javascript
var dlg = $dialog.create();
dlg.标题("提示");
dlg.内容("我是一个对话框");
dlg.show();   //最后调它才会显示
```


### showBefore(callback)

> 设定一个“刚要显示之前”就执行的函数（在界面线程里跑）。
> 
> 返回对话框自己，可链式继续设置。

- 参数 : callback {Function} 显示前执行的函数，形如 function() {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用
- 版本 : 1.5.0


```javascript
$dialog.create()
    .标题("提示")
    .内容("我是一个对话框")
    .showBefore(function() {
        log("对话框显示前回调");
    })
    .show();
```


### showAfter(callback)

> 设定一个“刚显示出来之后”就执行的函数（在界面线程里跑）。
> 
> 最常用于：自定义视图放进去后，在里面给按钮绑点击事件（这时视图才真正可用）。
> 返回对话框自己，可链式继续设置。

- 参数 : callback {Function} 显示后执行的函数，形如 function() {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用
- 版本 : 1.5.0


```javascript
var ui = $ui.layout("ui.xml");        //解析一个自定义视图
var dlg = $dialog.create();
dlg.showAfter(function() {
    var but = ui.id("mButtonClose");   //视图显示后再取里面的按钮
    but.click(function() {
        dlg.close();                  //点它就关闭对话框
    });
}).view(ui.getView()).show();
```


### onClose(callback)

> 设定一个“这个对话框被关闭时”要执行的函数。
> 
> 不管是点按钮、按返回键还是代码里调 close()，只要弹框消失了就会执行它。

- 参数 : callback {Function} 关闭时执行的函数，形如 function() {}
- 版本 : 1.8.0


```javascript
var dlg = $dialog.create()
    .标题("标题")
    .内容("我是信息")
    .按钮3("关闭", function() {
        dlg.close();   //这里关闭对话框
    });
dlg.onClose(function() {
    log("对话框被关闭了");   //弹框一消失就执行这里
});
dlg.show();
```


### close()

> 手动关闭这个正在显示的对话框。
> 
> 没在显示时调用也没影响。


```javascript
var dlg = $dialog.create()
    .标题("提示")
    .内容("我是一个对话框")
    .按钮1("关闭", function() {
        dlg.close();   //这里关闭对话框
    });
dlg.show();
```


