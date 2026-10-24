# AdjFloaty - 可调节悬浮窗

- 更新时间:2026-10-22 10:55:49

> 一个可以自由拖动、还能调节大小的悬浮窗。
> 
> 它在屏幕上飘着，你可以用手指按住标题栏把它拖到任意位置，拖边缘的把手来改变大小，
> 还能调透明度、随时关掉。脚本里一般用 $floaty.newAdj("布局文件") 来创建并显示它。
> 创建好后，用 id("控件id") 找到里面放的按钮、文字等控件，就能给它们加点击事件了。



```javascript
var adj = $floaty.newAdj("main.xml");  //按 main.xml 布局创建一个可调节悬浮窗
var btn = adj.id("button_close");      //在悬浮窗里找 id 为 button_close 的控件
btn.点击事件(function(){               //给按钮加点击事件（用 function，不要用箭头函数）
    adj.close();                       //点了就关闭这个悬浮窗
});
```




### const {WindowManager.LayoutParams} params;

> 这个悬浮窗在系统里的窗口参数（WindowManager.LayoutParams）。
> 
> 它记录了悬浮窗的位置、宽高、窗口类型等底层信息。普通用户一般不需要动它，这里保留给需要深度定制的人。

- 版本 : 1.5.4


```javascript
var adj = $floaty.newAdj("main.xml");   //创建一个可调节悬浮窗
log(adj.params);                        //打印它的窗口参数（高级用户才改）
```


### const {WindowManager} manager;

> 系统的悬浮窗管理器（WindowManager）。
> 
> 负责把这个悬浮窗添加到屏幕上、更新位置或移除。普通用户一般不需要直接碰它。

- 版本 : 1.5.4


```javascript
var adj = $floaty.newAdj("main.xml");   //创建一个可调节悬浮窗
log(adj.manager);                       //打印系统悬浮窗管理器
```


### id(id)

> 在这个悬浮窗里，按控件 id 找到对应的控件（XView）。
> 
> 悬浮窗里放了按钮、文字等控件后，用这个方法按它们的 id 把对象取出来，才能进一步给它加事件、改文字。
> 找不到时返回 null。

- 参数 : id {String} 要找的控件 id 字符串，比如 "button_close"
- 返回 : {XView} 找到的控件对象；找不到时返回 null


```javascript
var adj = $floaty.newAdj("main.xml");  //创建可调节悬浮窗
var but = adj.id("button_close");      //找 id 为 button_close 的控件
if (but != null) {
    but.点击事件(function(){ adj.close(); }); //点它就关闭悬浮窗
}
```


### close()

> 关闭并销毁这个悬浮窗。
> 
> 调用后悬浮窗会从屏幕上消失，相关资源也会被释放；之后就不能再用了。


```javascript
var adj = $floaty.newAdj("main.xml");  //创建可调节悬浮窗
var but = adj.id("button_close");      //找关闭按钮
but.点击事件(function(){               //点按钮后关闭悬浮窗
    adj.close();
});
```


### getW()

> 读取这个悬浮窗当前的宽度（像素，整数）。

- 返回 : {int} 悬浮窗当前宽度（像素）


```javascript
var adj = $floaty.newAdj("main.xml");  //创建可调节悬浮窗
sleep(1000);                          //等它显示出来
var w = adj.getW();                    //读取当前宽度
log("宽度：" + w);
```


### getX()

> 读取这个悬浮窗左上角的 X 坐标（像素，整数）。
> 
> 也就是悬浮窗左边离屏幕左边缘的距离。

- 返回 : {int} 悬浮窗的 X 坐标（像素）


```javascript
var adj = $floaty.newAdj("main.xml");  //创建可调节悬浮窗
var x = adj.getX();                    //读取 X 坐标
log("X坐标：" + x);
```


### getY()

> 读取这个悬浮窗左上角的 Y 坐标（像素，整数）。
> 
> 也就是悬浮窗上边离屏幕顶部的距离。

- 返回 : {int} 悬浮窗的 Y 坐标（像素）


```javascript
var adj = $floaty.newAdj("main.xml");  //创建可调节悬浮窗
var y = adj.getY();                    //读取 Y 坐标
log("Y坐标：" + y);
```


### getH()

> 读取这个悬浮窗当前的高度（像素，整数）。

- 返回 : {int} 悬浮窗当前高度（像素）


```javascript
var adj = $floaty.newAdj("main.xml");  //创建可调节悬浮窗
sleep(1000);                          //等它显示出来
var h = adj.getH();                    //读取当前高度
log("高度：" + h);
```


