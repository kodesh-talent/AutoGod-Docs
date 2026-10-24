# $tip - 阻塞式对话框

- 更新时间:2026-10-22 10:55:52

> $tip：一系列会"卡住脚本"的弹窗工具。
> 
> 包括信息提示、输入框、整数输入、确认框、自定义布局、单选/多选列表、日期和时间选择。
> 调用这些方法后脚本会暂停，等用户在弹窗里操作完（点确定/取消/选好）才继续往下跑，
> 所以很适合做"需要用户确认一步再走下一步"的顺序流程。



```javascript
// 弹一个提示框，脚本会等用户关闭后再继续
$tip.show("Notice", "Task completed");
```




### i(msg)

> 弹出一个标题为"信息"的提示框，显示你给的内容。
> 
> 可以一次传多个参数，会自动拼到一起。用来给用户看普通说明。

- 参数 : msg {Object...} 要显示的内容，可传多个
- 版本 : 1.0.0


```javascript
// 弹一个信息框
$tip.i("我是信息");
```


### v(msg)

> 弹出一个标题为"说明"的提示框，显示内容。
> 
> 跟 i 类似，只是标题不同，用来放一些次要的说明文字。

- 参数 : msg {Object...} 要显示的内容，可传多个
- 版本 : 1.0.0


```javascript
// 弹一个说明框
$tip.v("我是信息");
```


### w(msg)

> 弹出一个标题为"警告"的提示框，提醒用户注意。

- 参数 : msg {Object...} 警告内容，可传多个
- 版本 : 1.0.0


```javascript
// 弹一个警告框
$tip.w("我是警告");
```


### e(msg)

> 弹出一个标题为"异常"的提示框，用来报错或提示出错。

- 参数 : msg {Object...} 异常内容，可传多个
- 版本 : 1.0.0


```javascript
// 弹一个异常框
$tip.e("出错了");
```


### d(msg)

> 弹出一个标题为"调试"的提示框，放调试用的临时信息。

- 参数 : msg {Object...} 调试内容，可传多个
- 版本 : 1.0.0


```javascript
// 调试时弹个框看中间值
$tip.d("当前进度：50%");
```


### input(title, callback)

> 弹出一个输入框对话框，让用户输入一段文字。
> 
> 用户点确定后，输入的文字会通过回调传出来；用户取消则不回调。

- 参数 : title {string} 对话框标题
- 参数 : callback {function(value){}} 用户输入完成后的回调，参数是输入的文字
- 版本 : 1.0.0


```javascript
// 弹输入框，拿到用户输入的内容
$tip.input("请输入你的名字", function(value) {
    toast("你输入的是：" + value);
});
```


### input(title, def, callback)

> 弹出带默认值的输入框对话框。
> 
> 第二个参数是输入框里预先填好的默认文字，用户可以直接改或直接确定。

- 参数 : title {string} 对话框标题
- 参数 : def {string} 输入框默认文字
- 参数 : callback {function(value){}} 输入完成回调
- 版本 : 1.0.0


```javascript
// 输入框里默认填好"张三"
$tip.input("请输入你的名字", "张三", function(value) {
    toast("你输入的是：" + value);
});
```


### input(title, hint, def, callback)

> 弹出最完整的输入框：可同时设置标题、占位提示文字和默认值。
> 
> hint 是输入框为空时显示的灰色提示文字，def 是预填内容。

- 参数 : title {string} 对话框标题
- 参数 : hint {string} 输入框占位提示文字
- 参数 : def {string} 输入框默认文字
- 参数 : callback {function(value){}} 输入完成回调
- 版本 : 1.0.0


```javascript
// 标题"你是?"，输入框提示"输入名字"，默认填"张三"
$tip.input("你是?", "输入名字", "张三", function(value) {
    toast("你输入的是：" + value);
});
```


### inputInt(title, callback)

> 弹出一个只能输入整数的输入框对话框。
> 
> 用户确定后把输入的数字通过回调传出来；如果最后没法解析成数字，回调结果为 0。
> 引导文字默认就是标题，默认值为 0。

- 参数 : title {string} 对话框标题
- 参数 : callback {function(num){}} 输入完成回调，参数是整数


```javascript
// 让用户输入年龄
$tip.inputInt("年龄", function(num) {
    toast("刚满" + num + "岁~");
});
```


### inputInt(title, def, callback)

> 弹出带默认数字的整数输入框。
> 
> 第二个参数是预填的默认数字。无法解析时回调为 0。

- 参数 : title {string} 对话框标题
- 参数 : def {int} 默认数字
- 参数 : callback {function(num){}} 输入完成回调


```javascript
// 默认填 18
$tip.inputInt("年龄", 18, function(num) {
    toast("刚满" + num + "岁~");
});
```


### inputInt(title, hint, callback)

> 弹出带占位提示文字的整数输入框（默认值为 0）。

- 参数 : title {string} 对话框标题
- 参数 : hint {string} 输入框占位提示文字
- 参数 : callback {function(num){}} 输入完成回调


```javascript
// 提示文字"请输入年龄:"
$tip.inputInt("年龄", "请输入年龄:", function(num) {
    toast("刚满" + num + "岁~");
});
```


### inputInt(title, hint, def, callback)

> 最完整的整数输入框：可同时设标题、占位提示和默认数字。

- 参数 : title {string} 对话框标题
- 参数 : hint {string} 输入框占位提示文字
- 参数 : def {int} 默认数字
- 参数 : callback {function(num){}} 输入完成回调


```javascript
// 标题"年龄"，提示"请输入你的年龄:"，默认 18
$tip.inputInt("年龄", "请输入你的年龄:", 18, function(num) {
    toast("刚满" + num + "岁~");
});
```


### show(title, msg)

> 弹出一个带标题和正文的普通提示框。
> 
> 这个弹窗会卡住脚本，直到用户把它关掉才继续往下跑。

- 参数 : title {string} 对话框标题
- 参数 : msg {string} 对话框正文内容
- 版本 : 1.0.0


```javascript
// 弹一个提示框
$tip.show("你好新人", "我是你的AIGame助手");
```


### show(title, msg, click)

> 弹出带"取消/确定"两个按钮的提示框，点确定后执行回调。
> 
> 点取消直接关闭；点确定先关闭再运行 click 里的函数。

- 参数 : title {string} 对话框标题
- 参数 : msg {string} 正文内容
- 参数 : click {function(){}} 点"确定"后执行的回调
- 版本 : 1.0.0


```javascript
// 弹确认框，点确定后 toast
$tip.show("你好新人", "我是你的AIGame助手", function() {
    toast("你好!");
});
```


### show(title, view)

> 弹出自定义布局的对话框，内容由你用 $ui 加载的 XML 视图决定。
> 
> 这种方式不显示底部按钮，右上角有关闭。同样会阻塞脚本直到关闭。

- 参数 : title {string} 对话框标题
- 参数 : view {View} 用 $ui 加载得到的视图对象
- 版本 : 1.0.0


```javascript
// 用 $ui 加载一个自定义布局
var ui = $ui.layout("ag-app-example/$tip - 阻塞式对话框/01.自定义对话框/ui.xml");
// 取出它的视图
var view = ui.getView();
// 把这个视图塞进对话框
$tip.show("自定义对话框", view);
```


### show(title, view, click)

> 弹出自定义布局对话框，并带一个"确定"按钮。
> 
> 点确定后关闭弹窗并执行 click 回调。

- 参数 : title {string} 对话框标题
- 参数 : view {View} $ui 加载的视图
- 参数 : click {function(){}} 点"确定"后的回调
- 版本 : 1.0.0


```javascript
var ui = $ui.layout("ag-app-example/$tip - 阻塞式对话框/01.自定义对话框/ui.xml");
var view = ui.getView();
// 自定义视图 + 确定按钮
$tip.show("自定义对话框", view, function() {
    toast("保存成功");
});
```


### one(title, items, callback)

> 弹出一个列表，让用户从多个选项里选一个。
> 
> 点中哪一项就把那项的文字通过回调传出来，并自动关闭弹窗。

- 参数 : title {string} 对话框标题
- 参数 : items {list[string]} 可选项文字数组
- 参数 : callback {function(value){}} 选中后的回调，参数是选中的文字
- 版本 : 1.0.0


```javascript
// 准备一个选项数组
var arr = ["小狗", "小猫", "小猪"];
// 弹出单选列表
$tip.one("请选择", arr, function(value) {
    toast("你选择了：" + value);
});
```


### more(title, items, callback)

> 弹出带复选框的列表，让用户一次选多个。
> 
> 选好后点"确定"，把选中的所有项组成数组通过回调传出来。

- 参数 : title {string} 对话框标题
- 参数 : items {list[string]} 可选项文字数组
- 参数 : callback {function(values){}} 确定后的回调，参数是选中项数组
- 版本 : 1.0.0


```javascript
var arr = ["小狗", "小猫", "小猪"];
// 弹出多选列表
$tip.more("请选择", arr, function(values) {
    // values 是选中项组成的数组
    toast("你选择了：" + values);
});
```


### calendar(callback)

> 弹出日历样式的日期选择器，选一个年月日。
> 
> 选好后回调拿到一个 DateInfo 对象，里面有 year(年)、month(月)、day(日)。
> 注意：这个回调跑在子线程里。

- 参数 : callback {function(dateInfo){}} 选完日期的回调，参数是含 year/month/day 的对象
- 版本 : 1.7.0


```javascript
// 弹出日历选日期
$tip.calendar(function(info) {
    var year = info.year;   // 年
    var month = info.month; // 月
    var day = info.day;     // 日
    // 拼起来显示
    toast(year + "-" + month + "-" + day);
});
```


### date(callback)

> 弹出滚轮样式的日期选择器，滚动选年月日。
> 
> 跟 calendar 类似，只是外观是滚轮；选完回调同样给 year/month/day。

- 参数 : callback {function(dateInfo){}} 选完日期回调，含 year/month/day
- 版本 : 1.2.8


```javascript
// 滚轮选日期
$tip.date(function(info) {
    var year = info.year;
    var month = info.month;
    var day = info.day;
    toast(year + "-" + month + "-" + day);
});
```


### clock(callback)

> 弹出 24 小时制的时钟选择器，选时和分。
> 
> 选好后回调拿到一个 TimeInfo 对象，里面有 hour(时)、minute(分)。回调在子线程。

- 参数 : callback {function(timeInfo){}} 选完时间回调，含 hour/minute
- 版本 : 1.7.0


```javascript
// 24 小时制选时间
$tip.clock(function(info) {
    var hour = info.hour;     // 时
    var minute = info.minute; // 分
    toast(hour + ":" + minute);
});
```


### time(callback)

> 弹出滚轮样式的 24 小时制时间选择器，滚动选时和分。
> 
> 跟 clock 类似，只是外观是滚轮；选完回调给 hour/minute。

- 参数 : callback {function(timeInfo){}} 选完时间回调，含 hour/minute
- 版本 : 1.2.8


```javascript
// 滚轮选时间
$tip.time(function(info) {
    var hour = info.hour;
    var minute = info.minute;
    toast(hour + ":" + minute);
});
```


