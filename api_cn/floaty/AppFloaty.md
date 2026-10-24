# AppFloaty - 应用级悬浮窗

- 更新时间:2026-10-22 10:55:49

> 应用级悬浮窗。
> 
> 它是一个可以浮在其他 App 上面的小窗口，用来放自己的按钮、文字、开关等界面。
> 可以自由设置位置、宽高、是否全屏、是否能被手指点到，还能监听屏幕横竖屏切换。
> 脚本里一般用 $floaty.newApp("布局文件") 创建并显示；创建后用 id("控件id") 找里面的控件。
> 注意：设置位置、大小的那些方法都会把悬浮窗自己返回，所以可以一串连着写（链式调用）。



```javascript
var floaty = $floaty.newApp("main.xml");    //按 main.xml 创建应用级悬浮窗
floaty.setXY(100, 200);                   //把它挪到 (100,200)
var btn = floaty.id("btn_close");         //找里面的关闭按钮
btn.点击事件(function(){                   //点按钮就关闭悬浮窗
    floaty.close();
});
```




### const {WindowManager.LayoutParams} params;

> 这个悬浮窗在系统里的窗口参数（WindowManager.LayoutParams）。
> 
> 记录悬浮窗的位置、宽高、窗口类型等底层信息，是公开字段，可以直接读改。
> 普通用户一般用 setX/setY/setW 这些方法就够了，不需要直接动它。

- 版本 : 1.3.5


```javascript
var floaty = $floaty.newApp("main.xml");   //创建一个应用级悬浮窗
log(floaty.params);                        //打印它的窗口参数（高级用户才改）
```


### const {WindowManager} manager;

> 系统的悬浮窗管理器（WindowManager）。
> 
> 负责把这个悬浮窗加到屏幕上、更新位置或移除。普通用户一般不需要直接碰它。

- 版本 : 1.3.5


```javascript
var floaty = $floaty.newApp("main.xml");   //创建一个应用级悬浮窗
log(floaty.manager);                       //打印系统悬浮窗管理器
```


### 监听屏幕旋转(回调)

> 注册“屏幕横竖屏切换时”的回调（中文写法）。
> 
> 和 onScreenChange 完全一样，只是方法名是中文。

- 参数 : 回调 {Function} 屏幕旋转时要执行的函数，会收到一个 ScreenInfo 屏幕信息参数
- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");
//屏幕旋转时回调，屏幕信息 是最新的屏幕信息对象
悬浮窗.监听屏幕旋转(function(屏幕信息) {
    悬浮窗.全屏(true); //旋转后让它全屏
});
```


### 找控件(标识)

> 在这个悬浮窗里，按控件 id 找到对应的控件（XView，中文写法）。
> 
> 和 id 完全一样，只是方法名是中文。找不到时返回 null。

- 参数 : 标识 {String} 要找的控件 id 字符串
- 返回 : {XView} 找到的控件对象；找不到时返回 null
- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");        //创建悬浮窗
var 关闭按钮 = 悬浮窗.找控件("关闭按钮");        //按 id 找关闭按钮
if (关闭按钮 != null) {
    关闭按钮.点击事件(function(){               //点它就关闭悬浮窗
        悬浮窗.关闭();
    });
}
```


### 全屏(是否全屏)

> 设置悬浮窗是否铺满整个屏幕（全屏，中文写法）。
> 
> 和 fill 完全一样，只是方法名是中文。传 true 全屏，false 按内容大小。

- 参数 : 是否全屏 {boolean} true 表示全屏铺满，false 表示按内容大小
- 返回 : {AppFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");  //创建悬浮窗
悬浮窗.全屏(true);                       //让它全屏显示
```


### 触摸(是否可触摸)

> 设置悬浮窗能不能被手指点到（中文写法）。
> 
> 和 touch 完全一样，只是方法名是中文。true 可点，false 不可触摸（点击穿透）。

- 参数 : 是否可触摸 {boolean} true 表示可以点，false 表示不可触摸
- 返回 : {AppFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");  //创建悬浮窗
悬浮窗.触摸(false);                      //设置成不可触摸
```


### 设置x(x)

> 设置悬浮窗左上角的 X 坐标（中文写法）。
> 
> 和 setX 完全一样，只是方法名是中文。

- 参数 : x {int} 新的 X 坐标（像素）
- 返回 : {AppFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");  //创建悬浮窗
悬浮窗.设置x(100);                      //把左边移到离屏幕左缘 100 像素
```


### 设置y(y)

> 设置悬浮窗左上角的 Y 坐标（中文写法）。
> 
> 和 setY 完全一样，只是方法名是中文。

- 参数 : y {int} 新的 Y 坐标（像素）
- 返回 : {AppFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");  //创建悬浮窗
悬浮窗.设置y(200);                      //把上边移到离屏幕顶部 200 像素
```


### 设置位置(x, y)

> 一次同时设置悬浮窗的 X、Y 坐标（位置，中文写法）。
> 
> 和 setXY 完全一样，只是方法名是中文。

- 参数 : x {int} 新的 X 坐标（像素）
- 参数 : y {int} 新的 Y 坐标（像素）
- 返回 : {AppFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");  //创建悬浮窗
悬浮窗.设置位置(100, 100);              //一次把位置设到 (100,100)
```


### 设置宽度(宽度)

> 设置悬浮窗的宽度（中文写法）。
> 
> 和 setW 完全一样，只是方法名是中文。

- 参数 : 宽度 {int} 新的宽度（像素）
- 返回 : {AppFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");  //创建悬浮窗
悬浮窗.设置宽度(300);                   //把宽度设为 300 像素
```


### 设置高度(高度)

> 设置悬浮窗的高度（中文写法）。
> 
> 和 setH 完全一样，只是方法名是中文。

- 参数 : 高度 {int} 新的高度（像素）
- 返回 : {AppFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");  //创建悬浮窗
悬浮窗.设置高度(200);                   //把高度设为 200 像素
```


### 设置宽高(宽度, 高度)

> 一次同时设置悬浮窗的宽度和高度（中文写法）。
> 
> 和 setWH 完全一样，只是方法名是中文。

- 参数 : 宽度 {int} 新的宽度（像素）
- 参数 : 高度 {int} 新的高度（像素）
- 返回 : {AppFloaty} 悬浮窗自己，方便链式继续调用
- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");  //创建悬浮窗
悬浮窗.设置宽高(300, 200);              //宽设 300、高设 200
```


### 断言()

> 检查这个悬浮窗现在还能不能用（中文写法）。
> 
> 和 check 完全一样，只是方法名是中文。true 表示还能用，false 表示已经关闭。

- 返回 : {boolean} 还能正常用返回 true；已关闭或不可用返回 false
- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");  //创建悬浮窗
if (悬浮窗.断言()) {                    //先检查还在不在
    log("悬浮窗还在，可以操作");
} else {
    log("悬浮窗已经关闭了");
}
```


### 关闭()

> 关闭并销毁这个悬浮窗（中文写法）。
> 
> 和 close 完全一样，只是方法名是中文。

- 版本 : 1.7.0


```javascript
var 悬浮窗 = $floaty.newApp("main.xml");  //创建悬浮窗
sleep(3000);                            //显示 3 秒
悬浮窗.关闭();                          //然后关闭悬浮窗
```


