# $alert - 原生对话框

- 更新时间:2026-10-22 10:55:52

> 原生提示框（对话框）。
> 
> 用来在屏幕中间弹出一个系统风格的小窗口，可以放标题、一段说明文字、几个按钮，
> 或者让用户从一组选项里选一个。它是“链式”用法：先 create() 创建，
> 接着一路 .标题(...)、.内容(...)、.按钮3(...) 把内容设好，最后 .显示() 弹出来。
> 每设一样东西都会把自己返回，所以可以一行串到底。



```javascript
var alt = $alert.create();              //创建一个提示框
alt.标题("确认");                        //设置标题
alt.内容("确定要继续吗？");             //设置正文
alt.按钮3("确定", function(){            //右侧按钮，点了执行这里
    log("点了确定");
});
alt.显示();                             //最后把它弹出来
```




### 创建()

> 创建一个新的提示框对象（中文写法）。
> 
> 和 create 完全一样，只是方法名是中文。

- 返回 : {AgAlert} 新建的提示框对象
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();  //创建一个提示框
```


### 标题(标题)

> 设置提示框顶部的标题文字（中文写法）。
> 
> 和 title 完全一样，只是方法名是中文。

- 参数 : 标题 {String} 标题文字
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.标题("温馨提示");   //设置对话框标题
```


### 是显示的()

> 检查这个提示框现在是否正显示在屏幕上（中文写法）。
> 
> 和 isShowing 完全一样，只是方法名是中文。

- 返回 : {boolean} 正在显示返回 true；没显示或已关闭返回 false
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
log(提示框.是显示的());   //还没显示，是 false
```


### 内容(内容)

> 设置提示框正文的内容文字（中文写法）。
> 
> 和 msg 完全一样，只是方法名是中文。

- 参数 : 内容 {String} 正文文字
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.内容("这里是要告诉用户的内容");   //设置正文
```


### 可取消(可取消)

> 设置用户能不能按返回键、或点弹窗外的空白处来关掉它（中文写法）。
> 
> 和 cancelable 完全一样，只是方法名是中文。

- 参数 : 可取消 {boolean} true 允许取消，false 不允许取消
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.可取消(false);   //设为不可随便取消，必须点按钮
```


### 图标(图标)

> 设置提示框标题左边的小图标（中文写法）。
> 
> 和 icon 完全一样，只是方法名是中文。

- 参数 : 图标 {String} 图标名或图片文件路径
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.图标("info");              //用图标库里名为 info 的图标
```


### 视图(视图)

> 用一个自定义视图（View）作为提示框的内容（中文写法）。
> 
> 和 view 完全一样，只是方法名是中文。

- 参数 : 视图 {View} 要放进提示框的自定义视图
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var ui = $ui.layout("main.xml");       //解析一个布局
var 视图 = ui.getView();              //拿到根视图
var 提示框 = $alert.create();
提示框.视图(视图);                     //把自定义视图放进提示框
```


### 视图(视图)

> 用一个 XView 控件作为提示框的内容（中文写法，重载）。
> 
> 和 view(XView) 完全一样，只是方法名是中文。

- 参数 : 视图 {XView} 要放进提示框的 XView 控件
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var ui = $ui.layout("main.xml");
var 视图 = ui.id("myView");        //按 id 取到一个 XView 控件
var 提示框 = $alert.create();
提示框.视图(视图);                 //把它放进提示框
```


### 最大高度(是否最大)

> 让提示框的高度尽量撑满到屏幕允许的最大高度（中文写法）。
> 
> 和 maxH 完全一样，只是方法名是中文。

- 参数 : 是否最大 {boolean} true 高度拉到最大，false 恢复默认
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.最大高度(true);   //对话框高度尽量显示到最大
```


### 最大宽度(是否最大)

> 让提示框的宽度尽量撑满到屏幕允许的最大宽度（中文写法）。
> 
> 和 maxW 完全一样，只是方法名是中文。

- 参数 : 是否最大 {boolean} true 宽度拉到最大，false 恢复默认
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.最大宽度(true);   //对话框宽度尽量显示到最大
```


### 最大宽高(是否最大)

> 让提示框的宽和高都尽量撑满到屏幕允许的最大（中文写法）。
> 
> 和 maxWH 完全一样，只是方法名是中文。

- 参数 : 是否最大 {boolean} true 宽高都拉到最大，false 恢复默认
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.最大宽高(true);   //对话框宽高都尽量显示到最大
```


### 按钮1(文本)

> 设置第一个按钮（最左边那个），只显示文字（中文写法）。
> 
> 和 but1 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.按钮1("取消");   //设置第一个按钮的文字
```


### 按钮1(文本, 回调)

> 设置第一个按钮（最左边那个），并指定被点击时要做的事（中文写法，带回调）。
> 
> 和 but1(text, callback) 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 参数 : 回调 {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.按钮1("取消", function(dialog, which) {
    log("点了取消");   //用户点这个按钮时执行这里
});
```


### 按钮2(文本)

> 设置第二个按钮（中间那个），只显示文字（中文写法）。
> 
> 和 but2 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.按钮2("稍后提醒");   //设置第二个按钮的文字
```


### 按钮2(文本, 回调)

> 设置第二个按钮（中间那个），并指定被点击时要做的事（中文写法，带回调）。
> 
> 和 but2(text, callback) 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 参数 : 回调 {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.按钮2("稍后提醒", function(dialog, which) {
    log("点了稍后提醒");   //用户点这个按钮时执行这里
});
```


### 按钮3(文本)

> 设置第三个按钮（最右边那个，通常是“确定”），只显示文字（中文写法）。
> 
> 和 but3 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.按钮3("确定");   //设置第三个按钮的文字
```


### 按钮3(文本, 回调)

> 设置第三个按钮（最右边那个，通常是“确定”），并指定被点击时要做的事（中文写法，带回调）。
> 
> 和 but3(text, callback) 完全一样，只是方法名是中文。

- 参数 : 文本 {CharSequence} 按钮上显示的文字
- 参数 : 回调 {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create();
提示框.按钮3("确定", function(dialog, which) {
    log("点了确定");   //用户点这个按钮时执行这里
});
```


### 选项(选项, 回调)

> 把提示框内容变成一组可点的列表选项（中文写法）。
> 
> 和 items 完全一样，只是方法名是中文。

- 参数 : 选项 {String[]} 选项文字组成的数组
- 参数 : 回调 {Function} 点选项后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 菜单 = ["安卓", "苹果", "鸿蒙"];
var 提示框 = $alert.create();
提示框.选项(菜单, function(dialog, which) {
    log("你选了第 " + which + " 项");   //点哪一行，which 就是它的序号
});
```


### 单选(选项, 选中的下标, 回调)

> 把提示框内容变成一组单选选项（中文写法）。
> 
> 和 oneItems 完全一样，只是方法名是中文。

- 参数 : 选项 {String[]} 选项文字组成的数组
- 参数 : 选中的下标 {int} 默认选中项的序号（从 0 开始，-1 都不选）
- 参数 : 回调 {Function} 点选项后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 字号 = ["小", "中", "大"];
var 提示框 = $alert.create();
提示框.单选(字号, 1, function(dialog, which) {
    log("选了第 " + which + " 项");   //点哪一行，which 就是它的序号
});
```


### 多选(选项, 回调)

> 把提示框内容变成一组多选选项（中文写法）。
> 
> 和 moreItems(items, callback) 完全一样，只是方法名是中文。

- 参数 : 选项 {String[]} 选项文字组成的数组
- 参数 : 回调 {Function} 勾选变化时执行的函数，形如 function(dialog, which, isChecked) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 权限 = ["定位", "存储", "相机"];
var 提示框 = $alert.create();
提示框.多选(权限, function(dialog, which, isChecked) {
    log("第 " + which + " 项现在是：" + isChecked);
});
```


### 多选(选项, 选中状态, 回调)

> 把提示框内容变成一组多选选项，并指定每一项默认勾不勾（中文写法，重载）。
> 
> 和 moreItems(items, checkedItems, callback) 完全一样，只是方法名是中文。

- 参数 : 选项 {String[]} 选项文字组成的数组
- 参数 : 选中状态 {boolean[]} 每一项的初始勾选状态，长度和选项数组一致
- 参数 : 回调 {Function} 勾选变化时执行的函数，形如 function(dialog, which, isChecked) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var 权限 = ["定位", "存储", "相机"];
var 默认勾 = [true, false, false];   //默认只勾第 0 项“定位”
var 提示框 = $alert.create();
提示框.多选(权限, 默认勾, function(dialog, which, isChecked) {
    log("第 " + which + " 项现在是：" + isChecked);
});
```


### 显示()

> 把设置好的提示框真正显示到屏幕上（中文写法）。
> 
> 和 show 完全一样，只是方法名是中文。通常一行链式调到底，最后用它收尾。

- 返回 : {AlertDialog} 系统对话框对象本身，一般不用接
- 版本 : 1.7.0


```javascript
$alert.create()
    .标题("标题")
    .内容("我是信息")
    .按钮3("确定", function() {
        log("我被点击了");
    })
    .显示();   //显示对话框
```


### 显示之前(回调)

> 设定一个“刚要显示之前”就执行的函数（中文写法）。
> 
> 和 showBefore 完全一样，只是方法名是中文。该回调在界面线程中执行。

- 参数 : 回调 {Function} 显示前执行的函数，形如 function() {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
$alert.create()
    .标题("标题")
    .内容("我是信息")
    .按钮3("确定", function() {
        log("我被点击了");
    })
    .显示之前(function() {
        log("准备显示对话框啦");
    })
    .显示();
```


### 显示之后(回调)

> 设定一个“刚显示出来之后”就执行的函数（中文写法）。
> 
> 和 showAfter 完全一样，只是方法名是中文。该回调在界面线程中执行。

- 参数 : 回调 {Function} 显示后执行的函数，形如 function() {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.7.0


```javascript
var ui = $ui.layout("ui.xml");       //解析一个自定义布局
var 提示框 = $alert.create();
提示框.显示之后(function() {
    var 关闭按钮 = ui.id("关闭按钮");   //视图显示后再取里面的按钮
    关闭按钮.click(function() {
        提示框.close();   //点它就关闭提示框
    });
}).视图(ui.getView()).显示();
```


### 监听关闭(回调)

> 设定一个“这个提示框被关闭时”要执行的函数（中文写法）。
> 
> 和 onClose 完全一样，只是方法名是中文。

- 参数 : 回调 {Function} 关闭时执行的函数，形如 function() {}
- 版本 : 1.8.0


```javascript
var 提示框 = $alert.create()
    .标题("标题")
    .内容("我是信息")
    .按钮3("关闭", function() {
        提示框.close();   //这里关闭提示框
    });
提示框.监听关闭(function() {
    log("对话框被关闭了");   //弹框一消失就执行这里
});
提示框.显示();
```


### 关闭()

> 手动关闭这个正在显示的提示框（中文写法）。
> 
> 和 close 完全一样，只是方法名是中文。

- 版本 : 1.7.0


```javascript
var 提示框 = $alert.create()
    .标题("标题")
    .内容("我是信息")
    .按钮3("关闭", function() {
        提示框.close();   //这里关闭对话框
    });
提示框.显示();
```


