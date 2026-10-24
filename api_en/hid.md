# $hid - 键鼠触控

- 更新时间:2026-10-22 10:55:49

> HID 键盘、鼠标和触控设备 API，通过已连接的外设模拟输入事件。
> 



```javascript
var ready = $hid.isOn();
```




### init()

> 初始化 HID 连接

- 返回 : {String} 初始化成功时返回 true，否则返回失败原因。
- 版本 : 1.8.9


```javascript
var res = $hid.init();
if(res=="true"){
    log("初始化成功");
}else{
    log("初始化失败:",res);
}
```


### isOn()

> 检查 HID 是否已启用
> 
> 检查硬件是否已连接。

- 返回 : {boolean} HID 是否已启用
- 版本 : 1.8.9


```javascript
if($hid.isOn()){
    log("处于开启状态");
}
```


### dexBeat()

> 获取版本
> 
> 获取插件版本。

- 返回 : {float} 版本号，以小数表示。
- 版本 : 1.8.9


```javascript
log("HID版本:",$hid.dexBeat());
```


### getBatteryLevel()

> 获取电池电量
> 
> 获取当前手机电池电量。

- 返回 : {int} 电池电量数值。
- 版本 : 1.8.9


```javascript
log("电池电量:",$hid.getBatteryLevel());
```


### isCharging()

> 检查手机是否正在充电
> 
> 检查手机当前是否正在充电。

- 返回 : {boolean} 检查手机是否正在充电
- 版本 : 1.8.9


```javascript
if($hid.isCharging()){
    log("正在充电...");
}
```


### setPowerOff()

> 关闭外设的供电输出。

- 版本 : 1.8.9


```javascript
$hid.setPowerOff();
```


### setPowerOn()

> 打开电源输出

- 版本 : 1.8.9


```javascript
$hid.setPowerOn();
```


### click(x, y)

> Performs a tap.

- 参数 : x {int} X coordinate
- 参数 : y {int} Y coordinate
- 返回 : {boolean} 点击是否成功。
- 版本 : 1.8.9


```javascript
$hid.click(100,100);
```


### click(index)

> Performs a tap.

- 参数 : index {int[]} 坐标整数数组。
- 返回 : {boolean} 点击是否成功。
- 版本 : 1.8.9


```javascript
$hid.click([100,100]);
```


### longClick(x, y, dur)

> 模拟长按操作。

- 参数 : x {int} X coordinate
- 参数 : y {int} Y coordinate
- 参数 : dur {int} 长按持续时间。
- 返回 : {boolean} 点击是否成功。
- 版本 : 1.8.9


```javascript
$hid.longClick(100,100,1500);
```


### longClick(index)

> 模拟长按操作。

- 参数 : index {int[]} 坐标整数数组。
- 返回 : {boolean} 点击是否成功。
- 版本 : 1.8.9


```javascript
$hid.longClick([100,100,1500]);
```


### swipEx(x1, y1, x2, y2)

> 执行增强滑动操作。

- 参数 : x1 {int} 起点 X 坐标
- 参数 : y1 {int} 起点 Y 坐标
- 参数 : x2 {int} 终点 X 坐标
- 参数 : y2 {int} 终点 Y 坐标
- 返回 : {boolean} 滑动是否成功
- 版本 : 1.8.9


```javascript
$hid.swipEx(100,100,200,200);
```


### swipEx(x1, y1, x2, y2, press, time, delay)

> 执行增强滑动操作。

- 参数 : x1 {int} 起点 X 坐标
- 参数 : y1 {int} 起点 Y 坐标
- 参数 : x2 {int} 终点 X 坐标
- 参数 : y2 {int} 终点 Y 坐标
- 参数 : press {int} 按压时长（默认 300 毫秒）
- 参数 : time {int} 滑动时长（默认 1000 毫秒）
- 参数 : delay {int} 延迟时间（默认 0 毫秒）
- 返回 : {boolean} 滑动是否成功
- 版本 : 1.8.9


```javascript
$hid.swipEx(100,100,200,200,300,1000,0);
```


### touchDown(id, x, y)

> 按下触控点。

- 参数 : id {int} 手指编号
- 参数 : x {int} X coordinate
- 参数 : y {int} Y coordinate
- 返回 : {boolean} 按压是否成功
- 版本 : 1.8.9


```javascript
$hid.touchDown(0,100,100);
```


### touchMove(id, x, y)

> Moves a pointer

- 参数 : id {int} 手指编号
- 参数 : x {int} X coordinate
- 参数 : y {int} Y coordinate
- 返回 : {boolean} 移动是否成功
- 版本 : 1.8.9


```javascript
$hid.touchMove(0,100,100);
```


### touchUp(id)

> Lifts a pointer

- 参数 : id {int} 手指编号
- 返回 : {boolean} 手指是否已抬起
- 版本 : 1.8.9


```javascript
$hid.touchUp(0);
```


### keyPress(keyCode)

> Presses a key

- 参数 : keyCode {int} 按键代码
- 返回 : {boolean} 按压是否成功
- 版本 : 1.8.9


```javascript
$hid.keyPress(40);
```


### keyPress(modify, keyCode)

> Presses a key

- 参数 : modify {int} 修饰键编码。
- 参数 : keyCode {int} 按键代码
- 返回 : {boolean} 按压是否成功
- 版本 : 1.8.9


```javascript
$hid.keyPress(0,40);
```


### home()

> 模拟按下主屏幕键，返回桌面。
> 
> 按下手机 Home 键。

- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.home();
```


### back()

> 模拟按下返回键。
> 
> 按下手机返回键。

- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.back();
```


### recents()

> 模拟按下最近任务键。
> 
> 打开手机最近任务界面。

- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.recents();
```


### recentsV2()

> 执行增强的最近任务操作。
> 
> 对有特殊要求的设备使用备用方式打开最近任务。

- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.recentsV2();
```


### selectAll()

> 选择输入框中的全部文字。
> 
> 按下全选，将输入框中的全部文本选中。

- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.selectAll();
```


### cut()

> 剪切当前选中的文字。
> 
> 剪切输入框中的全部文本到剪贴板。

- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.cut();
```


### copy()

> 复制当前选中的文字。
> 
> 复制输入框中的全部文本到剪贴板。

- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.copy();
```


### paste()

> 粘贴剪贴板中的文字。
> 
> 将剪贴板文本粘贴到输入框，可配合写入剪贴板的命令使用。

- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
//先设置剪切板
$sys.setClip("我是来自剪切板的内容");
//再粘贴内容
$hid.paste();
```


### paste(text)

> 粘贴指定文字。
> 
> 将剪贴板文本粘贴到输入框，可配合写入剪贴板的命令使用。

- 参数 : text 要写入剪贴板并粘贴的文本
- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.paste("我是来自剪切板内容");
//等价于下面的写法
//1.先设置剪切板
$sys.setClip("我是来自剪切板的内容");
//2.再粘贴内容
$hid.paste();
```


### inputSimple(text)

> 输入指定文字。
> 
> 在输入框中输入英文字母和数字。
> 
> 不支持标点符号和中文字符。

- 参数 : text {String} 要输入的文字。
- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.inputSimple("abcd1234");
```


### delete()

> 删除输入框中的文字。
> 
> 通过删除键移除输入框中的文字；部分设备可能使用退格键。

- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.delete();
```


### delete(len)

> 删除输入框中的文字。
> 
> 通过删除键移除输入框中的文字；部分设备可能使用退格键。

- 参数 : len {int} 要删除的字符数量。
- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.delete(2);
```


### backspace()

> 使用退格键删除文字。
> 
> 通过退格键移除输入框中的文字；部分设备的实际按键行为可能不同。

- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.backspace();
```


### backspace(len)

> 使用退格键删除文字。
> 
> 通过退格键移除输入框中的文字；部分设备的实际按键行为可能不同。

- 参数 : len {int} 要删除的字符数量。
- 返回 : {boolean} 操作是否成功。
- 版本 : 1.8.9


```javascript
$hid.backspace(2);
```


