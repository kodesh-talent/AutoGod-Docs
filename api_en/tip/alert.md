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




### create()

> 创建一个新的提示框对象。
> 
> 每次想弹窗都先调它拿到一个全新的 AgAlert，再接着设置标题、内容、按钮，最后显示。

- 返回 : {AgAlert} 新建的提示框对象，可继续链式设置
- 版本 : 1.5.1


```javascript
var alt = $alert.create();  //创建一个提示框
```


### title(title)

> 设置提示框顶部的标题文字。
> 
> 传空字符串则不设置标题。返回提示框自己，可链式继续设置。

- 参数 : title {String} 标题文字
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.title("温馨提示");   //设置对话框标题
```


### isShowing()

> 检查这个提示框现在是否正显示在屏幕上。

- 返回 : {boolean} 正在显示返回 true；没显示或已关闭返回 false
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
log(alt.isShowing());   //还没显示，是 false
alt.显示();
log(alt.isShowing());   //显示后，是 true
```


### msg(msg)

> 设置提示框正文的内容文字。
> 
> 就是标题下面那段主要说明文字。传空则不显示。返回提示框自己，可链式继续设置。

- 参数 : msg {String} 正文文字
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.msg("这里是要告诉用户的内容");   //设置正文
```


### cancelable(cancelable)

> 设置用户能不能按返回键、或点弹窗外的空白处来关掉它。
> 
> 传 true，用户可以随便关掉（默认就是这样）；传 false，就只能靠点按钮才能关掉，常用于“必须做出选择”的场合。
> 返回提示框自己，可链式继续设置。

- 参数 : cancelable {boolean} true 允许取消，false 不允许取消
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.cancelable(false);   //设为不可随便取消，必须点按钮
```


### icon(icon)

> 设置提示框标题左边的小图标。
> 
> 传一个图标名字（图标库里有的）或一张图片的路径；找不到就不设置。
> 返回提示框自己，可链式继续设置。

- 参数 : icon {String} 图标名或图片文件路径
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.icon("info");              //用图标库里名为 info 的图标
//也可以传一个图片路径：
//alt.icon("/sdcard/ic_launcher.png");
```


### view(view)

> 用一个自定义视图（View）作为提示框的内容。
> 
> 不想只显示干巴巴的文字，而是想在弹框里放自己设计的界面（输入框、开关等）时，
> 先用 $ui.layout 加载一个布局拿到 View，再传给它。传进去后原来的正文会被清空。
> 返回提示框自己，可链式继续设置。

- 参数 : view {View} 要放进提示框的自定义视图
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
//先用 $ui 解析一个布局，拿到它的根视图
var ui = $ui.layout("main.xml");
var view = ui.getView();
var alt = $alert.create();
alt.view(view);              //把这个自定义视图放进提示框
```


### view(view)

> 用一个 XView 控件作为提示框的内容（重载）。
> 
> 和上面的 view(View) 类似，只是这里直接传一个用 $ui.id(...) 取到的 XView 控件。
> 传 null 会打印“视图(view)为空”的提示。返回提示框自己，可链式继续设置。

- 参数 : view {XView} 要放进提示框的 XView 控件
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var ui = $ui.layout("main.xml");
var xview = ui.id("myView");       //按 id 取到一个 XView 控件
var alt = $alert.create();
alt.view(xview);                  //把它放进提示框
```


### maxH(max)

> 让提示框的高度尽量撑满到屏幕允许的最大高度。
> 
> 内容很多、默认显示不全时，传 true 让它纵向尽量拉长。返回提示框自己，可链式继续设置。

- 参数 : max {boolean} true 高度拉到最大，false 恢复默认
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.maxH(true);   //对话框高度尽量显示到最大
```


### maxW(max)

> 让提示框的宽度尽量撑满到屏幕允许的最大宽度。
> 
> 返回提示框自己，可链式继续设置。

- 参数 : max {boolean} true 宽度拉到最大，false 恢复默认
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.maxW(true);   //对话框宽度尽量显示到最大
```


### maxWH(max)

> 让提示框的宽和高都尽量撑满到屏幕允许的最大。
> 
> 相当于同时打开最大宽度和最大高度。返回提示框自己，可链式继续设置。

- 参数 : max {boolean} true 宽高都拉到最大，false 恢复默认
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.maxWH(true);   //对话框宽高都尽量显示到最大
```


### but1(text)

> 设置第一个按钮（最左边那个），只显示文字，点了就关闭弹框、不做事。
> 
> 返回提示框自己，可链式继续设置。

- 参数 : text {CharSequence} 按钮上显示的文字
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.but1("取消");   //设置第一个按钮的文字
```


### but1(text, callback)

> 设置第一个按钮（最左边那个），并指定被点击时要做的事（带回调的重载）。
> 
> 第二个参数传一个函数，用户点了这个按钮就会在后台线程执行它。函数会收到
> (对话框, 按钮编号) 两个参数。

- 参数 : text {CharSequence} 按钮上显示的文字
- 参数 : callback {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.but1("取消", function(dialog, which) {
    log("点了取消");   //用户点这个按钮时执行这里
});
```


### but2(text)

> 设置第二个按钮（中间那个），只显示文字，点了就关闭弹框、不做事。
> 
> 返回提示框自己，可链式继续设置。

- 参数 : text {CharSequence} 按钮上显示的文字
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.but2("稍后提醒");   //设置第二个按钮的文字
```


### but2(text, callback)

> 设置第二个按钮（中间那个），并指定被点击时要做的事（带回调的重载）。
> 
> 第二个参数传一个函数，用户点了这个按钮就会在后台线程执行它。函数会收到
> (对话框, 按钮编号) 两个参数。

- 参数 : text {CharSequence} 按钮上显示的文字
- 参数 : callback {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.but2("稍后提醒", function(dialog, which) {
    log("点了稍后提醒");   //用户点这个按钮时执行这里
});
```


### but3(text)

> 设置第三个按钮（最右边那个，通常是“确定”），只显示文字，点了就关闭弹框、不做事。
> 
> 返回提示框自己，可链式继续设置。

- 参数 : text {CharSequence} 按钮上显示的文字
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.but3("确定");   //设置第三个按钮的文字
```


### but3(text, callback)

> 设置第三个按钮（最右边那个，通常是“确定”），并指定被点击时要做的事（带回调的重载）。
> 
> 第二个参数传一个函数，用户点了这个按钮就会在后台线程执行它。函数会收到
> (对话框, 按钮编号) 两个参数。

- 参数 : text {CharSequence} 按钮上显示的文字
- 参数 : callback {Function} 点击后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.but3("确定", function(dialog, which) {
    log("点了确定");   //用户点这个按钮时执行这里
});
```


### items(items, callback)

> 把提示框内容变成一组可点的列表选项（普通单选列表，没有勾选标记）。
> 
> 第一个参数传一个字符串数组，每一项就是列表里的一行；点某一行就会执行第二个参数的函数，
> 函数收到的 which 就是被点那一行的序号（从 0 开始）。
> 
> 注意：选项、单选、多选这三种列表方式互斥，同一次弹框只能用其中一种。

- 参数 : items {String[]} 选项文字组成的数组
- 参数 : callback {Function} 点选项后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var 菜单 = ["安卓", "苹果", "鸿蒙"];
var alt = $alert.create();
alt.items(菜单, function(dialog, which) {
    log("你选了第 " + which + " 项");   //点哪一行，which 就是它的序号
});
```


### oneItems(items, checkedItem, callback)

> 把提示框内容变成一组单选选项（每一行前面带一个圆圈，只能选中一个）。
> 
> 第二个参数是默认就选中哪一项的序号（从 0 开始，-1 表示都不选）；
> 点某一行时会执行第三个参数的函数，which 就是被选那行的序号。

- 参数 : items {String[]} 选项文字组成的数组
- 参数 : checkedItem {int} 默认选中项的序号（从 0 开始，-1 都不选）
- 参数 : callback {Function} 点选项后执行的函数，形如 function(dialog, which) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var 字号 = ["小", "中", "大"];
var alt = $alert.create();
alt.oneItems(字号, 1, function(dialog, which) {
    //默认选中第 1 项（“中”），点别的就把 which 传出来
    log("选了第 " + which + " 项");
});
```


### moreItems(items, callback)

> 把提示框内容变成一组多选选项（每一行前面带一个方框，可以同时勾多个）。
> 
> 默认所有项都不勾。点某一行时会执行第二个参数的函数，函数收到三个参数：
> (对话框, 被点那行的序号, 现在是勾上还是取消)。

- 参数 : items {String[]} 选项文字组成的数组
- 参数 : callback {Function} 勾选变化时执行的函数，形如 function(dialog, which, isChecked) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var 权限 = ["定位", "存储", "相机"];
var alt = $alert.create();
alt.moreItems(权限, function(dialog, which, isChecked) {
    //每勾或取消一行都会进来，which 是行号，isChecked 是现在的勾选状态
    log("第 " + which + " 项现在是：" + isChecked);
});
```


### moreItems(items, checkedItems, callback)

> 把提示框内容变成一组多选选项，并指定每一项默认勾不勾（重载）。
> 
> 第二个参数是一个布尔数组，长度要和选项数组一样，true 表示那一项默认就勾上。
> 之后点某一行会执行第三个参数的函数，收到 (对话框, 行号, 现在是否勾上)。

- 参数 : items {String[]} 选项文字组成的数组
- 参数 : checkedItems {boolean[]} 每一项的初始勾选状态，长度和选项数组一致
- 参数 : callback {Function} 勾选变化时执行的函数，形如 function(dialog, which, isChecked) {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
var 权限 = ["定位", "存储", "相机"];
var 默认勾 = [true, false, false];   //默认只勾第 0 项“定位”
var alt = $alert.create();
alt.moreItems(权限, 默认勾, function(dialog, which, isChecked) {
    log("第 " + which + " 项现在是：" + isChecked);
});
```


### show()

> 把设置好的提示框真正显示到屏幕上。
> 
> 前面所有 title/msg/按钮 等设置都是“先准备着”，必须调 show() 才会弹出来。
> 如果还没授予悬浮窗权限，会弹一句“请检查悬浮窗权限”的提示。

- 返回 : {AlertDialog} 系统对话框对象本身，一般不用接
- 版本 : 1.5.1


```javascript
var alt = $alert.create();
alt.标题("温馨提示");
alt.内容("准备好了吗？");
alt.按钮3("开始", function() {
    log("开始干活");
});
alt.show();   //最后调它才会显示
```


### showBefore(callback)

> 设定一个“刚要显示之前”就执行的函数。
> 
> 这个函数会在界面线程里、对话框真正弹出来之前跑一次。常用于显示前临时改点东西。
> 返回提示框自己，可链式继续设置。

- 参数 : callback {Function} 显示前执行的函数，形如 function() {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
$alert.create()
    .标题("标题")
    .内容("我是信息")
    .按钮3("确定", function() {
        log("我被点击了");
    })
    .showBefore(function() {
        log("准备显示对话框啦");   //弹出来之前执行这里
    })
    .show();
```


### showAfter(callback)

> 设定一个“刚显示出来之后”就执行的函数。
> 
> 这个函数会在界面线程里、对话框弹出来之后跑一次。最常用于：自定义视图放进去后，
> 在里面给按钮绑点击事件（这时视图才真正可用）。
> 返回提示框自己，可链式继续设置。

- 参数 : callback {Function} 显示后执行的函数，形如 function() {}
- 返回 : {AgAlert} 提示框自己，可链式继续调用
- 版本 : 1.5.1


```javascript
//先用 $ui 解析一个自定义布局
var ui = $ui.layout("ui.xml");
var mAlert = $alert.create();
mAlert.showAfter(function() {
    //视图显示出来后，再去取里面的按钮并绑定事件
    var but = ui.id("mButtonClose");
    but.click(function() {
        mAlert.close();   //点这个按钮就关闭提示框
    });
}).view(ui.getView()).show();
```


### onClose(callback)

> 设定一个“这个提示框被关闭时”要执行的函数。
> 
> 不管是用户点按钮、按返回键，还是代码里调 close()，只要弹框消失了就会执行它。

- 参数 : callback {Function} 关闭时执行的函数，形如 function() {}
- 版本 : 1.8.0


```javascript
var alt = $alert.create()
    .标题("标题")
    .内容("我是信息")
    .按钮3("关闭", function() {
        alt.close();   //这里关闭提示框
    });
alt.onClose(function() {
    log("对话框被关闭了");   //弹框一消失就执行这里
});
alt.show();
```


### close()

> 手动关闭这个正在显示的提示框。
> 
> 如果它没在显示，调用了也没影响。常用于自定义按钮里点一下就关。

- 版本 : 1.5.1


```javascript
var alt = $alert.create()
    .标题("标题")
    .内容("我是信息")
    .按钮3("关闭", function() {
        alt.close();   //这里关闭对话框
    });
alt.show();
```


