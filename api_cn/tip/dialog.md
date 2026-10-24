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




### 创建()

> 创建一个新的 M3 对话框对象（中文写法）。
> 
> 和 create 完全一样，只是方法名是中文。

- 返回 : {AgDialog} 新建的对话框对象


```javascript
var dlg = $dialog.create();  //创建一个对话框
```


### 标题(标题)

> 设置对话框顶部的标题文字（中文写法）。
> 
> 和 title 完全一样，只是方法名是中文。

- 参数 : 标题 {String} 标题文字
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.标题("温馨提示");   //设置对话框标题
```


### 是显示的()

> 检查这个对话框现在是否正显示在屏幕上（中文写法）。
> 
> 和 isShowing 完全一样，只是方法名是中文。

- 返回 : {boolean} 正在显示返回 true；没显示或已关闭返回 false


```javascript
var dlg = $dialog.create();
if (dlg.是显示的()) {
    log("对话框正在显示");
}
```


### 内容(内容)

> 设置对话框正文的内容文字（中文写法）。
> 
> 和 msg 完全一样，只是方法名是中文。

- 参数 : 内容 {String} 正文文字
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.内容("这里是要告诉用户的内容");   //设置正文
```


### 可取消(可取消)

> 设置用户能不能按返回键、或点弹窗外的空白处来关掉它（中文写法）。
> 
> 和 cancelable 完全一样，只是方法名是中文。

- 参数 : 可取消 {boolean} true 允许取消，false 不允许取消
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.可取消(false);   //设为不可随便取消，必须点按钮
```


### 图标(图标)

> 设置对话框标题左边的小图标（中文写法）。
> 
> 和 icon 完全一样，只是方法名是中文。

- 参数 : 图标 {String} 图标名或图片文件路径
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.图标("info");   //用图标库里名为 info 的图标
```


### 视图(视图)

> 用一个自定义视图（View）作为对话框的内容（中文写法）。
> 
> 和 view(View) 完全一样，只是方法名是中文。

- 参数 : 视图 {View} 要放进对话框的自定义视图
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var ui = $ui.layout("main.xml");
var 视图 = ui.getView();
var dlg = $dialog.create();
dlg.视图(视图);
```


### 视图(视图)

> 用一个 XView 控件作为对话框的内容（中文写法，重载）。
> 
> 和 view(XView) 完全一样，只是方法名是中文。

- 参数 : 视图 {XView} 要放进对话框的 XView 控件
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var ui = $ui.layout("main.xml");
var 视图 = ui.id("myView");
var dlg = $dialog.create();
dlg.视图(视图);
```


### 按钮1(文本)

> 设置第一个按钮（最左边那个），只显示文字（中文写法）。
> 
> 和 but1 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.按钮1("取消");
```


### 按钮1(文本, 回调)

> 设置第一个按钮（最左边那个），并指定被点击时要做的事（中文写法，带回调）。
> 
> 和 but1(text, callback) 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 参数 : 回调 {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.按钮1("取消", function(dialog, which) {
    log("我被点击了");
});
```


### 按钮2(文本)

> 设置第二个按钮（中间那个），只显示文字（中文写法）。
> 
> 和 but2 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.按钮2("稍后提醒");
```


### 按钮2(文本, 回调)

> 设置第二个按钮（中间那个），并指定被点击时要做的事（中文写法，带回调）。
> 
> 和 but2(text, callback) 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 参数 : 回调 {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.按钮2("稍后提醒", function(dialog, which) {
    log("我被点击了");
});
```


### 按钮3(文本)

> 设置第三个按钮（最右边那个，通常是“确定”），只显示文字（中文写法）。
> 
> 和 but3 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.按钮3("确定");
```


### 按钮3(文本, 回调)

> 设置第三个按钮（最右边那个，通常是“确定”），并指定被点击时要做的事（中文写法，带回调）。
> 
> 和 but3(text, callback) 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 参数 : 回调 {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var dlg = $dialog.create();
dlg.按钮3("确定", function(dialog, which) {
    log("我被点击了");
});
```


### 选项(选项, 回调)

> 把对话框内容变成一组可点的列表选项（中文写法）。
> 
> 和 items 完全一样，只是方法名是中文。

- 参数 : 选项 {String[]} 选项文字组成的数组
- 参数 : 回调 {Function} 点选项后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var 菜单 = ["安卓", "苹果", "鸿蒙"];
var dlg = $dialog.create();
dlg.选项(菜单, function(dialog, which) {
    log("你选了第 " + which + " 项");
}).显示();
```


### 单选(选项, 选中位置, 回调)

> 把对话框内容变成一组单选选项（中文写法）。
> 
> 和 oneItems 完全一样，只是方法名是中文。

- 参数 : 选项 {String[]} 选项文字组成的数组
- 参数 : 选中位置 {int} 默认选中项的序号（从 0 开始，-1 都不选）
- 参数 : 回调 {Function} 点选项后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var 字号 = ["小", "中", "大"];
var dlg = $dialog.create();
dlg.单选(字号, 1, function(dialog, which) {
    log("选了第 " + which + " 项");
}).显示();
```


### 多选(选项, 回调)

> 把对话框内容变成一组多选选项（中文写法）。
> 
> 和 moreItems(items, callback) 完全一样，只是方法名是中文。

- 参数 : 选项 {String[]} 选项文字组成的数组
- 参数 : 回调 {Function} 勾选变化时执行的函数，形如 function(dialog, which, isChecked) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var 权限 = ["定位", "存储", "相机"];
var dlg = $dialog.create();
dlg.多选(权限, function(dialog, which, isChecked) {
    log("第 " + which + " 项现在是：" + isChecked);
}).显示();
```


### 多选(选项, 选中项, 回调)

> 把对话框内容变成一组多选选项，并指定每一项默认勾不勾（中文写法，重载）。
> 
> 和 moreItems(items, checkedItems, callback) 完全一样，只是方法名是中文。

- 参数 : 选项 {String[]} 选项文字组成的数组
- 参数 : 选中项 {boolean[]} 每一项的初始勾选状态，长度和选项数组一致
- 参数 : 回调 {Function} 勾选变化时执行的函数，形如 function(dialog, which, isChecked) {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用


```javascript
var 权限 = ["定位", "存储", "相机"];
var 默认勾 = [true, false, false];
var dlg = $dialog.create();
dlg.多选(权限, 默认勾, function(dialog, which, isChecked) {
    log("第 " + which + " 项现在是：" + isChecked);
}).显示();
```


### 显示()

> 把设置好的对话框真正显示到屏幕上（中文写法）。
> 
> 和 show 完全一样，只是方法名是中文。

- 返回 : {AlertDialog} 系统对话框对象本身，一般不用接


```javascript
$dialog.create()
    .标题("提示")
    .内容("我是一个对话框")
    .显示();   //显示对话框
```


### 显示之前(回调)

> 设定一个“刚要显示之前”就执行的函数（中文写法）。
> 
> 和 showBefore 完全一样，只是方法名是中文。该回调在界面线程中执行。

- 参数 : 回调 {Function} 显示前执行的函数，形如 function() {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
$dialog.create()
    .标题("提示")
    .内容("我是一个对话框")
    .显示之前(function() {
        log("对话框显示前回调");
    })
    .显示();
```


### 显示之后(回调)

> 设定一个“刚显示出来之后”就执行的函数（中文写法）。
> 
> 和 showAfter 完全一样，只是方法名是中文。该回调在界面线程中执行。

- 参数 : 回调 {Function} 显示后执行的函数，形如 function() {}
- 返回 : {AgDialog} 对话框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var ui = $ui.layout("ui.xml");
var dlg = $dialog.create();
dlg.显示之后(function() {
    var 关闭按钮 = ui.id("关闭按钮");
    关闭按钮.click(function() {
        dlg.close();
    });
}).视图(ui.getView()).显示();
```


### 监听关闭(回调)

> 设定一个“这个对话框被关闭时”要执行的函数（中文写法）。
> 
> 和 onClose 完全一样，只是方法名是中文。

- 参数 : 回调 {Function} 关闭时执行的函数，形如 function() {}
- 版本 : 1.8.0


```javascript
var dlg = $dialog.create()
    .标题("标题")
    .内容("我是信息")
    .按钮3("关闭", function() {
        dlg.close();
    });
dlg.监听关闭(function() {
    log("对话框被关闭了");
});
dlg.显示();
```


### 关闭()

> 手动关闭这个正在显示的对话框（中文写法）。
> 
> 和 close 完全一样，只是方法名是中文。


```javascript
var dlg = $dialog.create()
    .标题("提示")
    .内容("我是一个对话框")
    .按钮1("关闭", function() {
        dlg.close();
    });
dlg.显示();
```


