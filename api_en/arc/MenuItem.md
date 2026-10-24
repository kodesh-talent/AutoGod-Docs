# MenuItem - 悬浮按钮

- 更新时间:2026-10-22 10:55:53

> 悬浮球上的一个圆形小按钮（MenuItem）。
> 
> 一个悬浮球里只有一个容器（MenuBody），但容器里可以放多个按钮。容器负责展开/收起动画，
> 按钮负责具体功能（点一下干什么）。用 $arc.item(图标) 创建一个按钮，用 样式/背景/图标颜色 等
> 方法把它打扮好看，再用 点击(...) 绑上要做的事，最后添加到容器里。所有设置方法都返回自己，可链式。



```javascript
var item = $arc.item("ic_settings");          //创建一个设置图标按钮
item.样式("outline").背景("#FF222222");        //设置样式和背景
item.click(function(clicked) {                 //点它要做的事
    log("点了设置按钮");
});
```




### style(style)

> 选择按钮的预设外观样式。
> 
> 可选三种："default" 实心、"outline" 描边轮廓、"tonal" 浅色填充。outline 也接受"轮廓""边框"，
> tonal 也接受"色调"；填别的名字就用 default。注意：换样式会重画按钮并清掉之前的颜色/圆角等外观，
> 所以要先定样式，再调颜色、圆角、提示、图标大小。

- 参数 : style 样式名：default、outline 或 tonal
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").style("outline");
item.bg("#55222222").iconTint("#FFFFFFFF");
```


### click(click)

> 设置点这个按钮时要执行的函数。
> 
> 传一个函数，函数会收到被点的那个按钮（MenuItem），并在后台线程里运行——
> 如果要在里面改界面，得自己切回界面线程。传 null 可清除之前绑的函数。

- 参数 : click 点击时执行的函数，形如 function(被点的按钮) {}；传 null 清除
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings");
item.click(function(clicked) {
    log("宽度=" + clicked.getW());
});
```


### ripper(color)

> 设置点按钮时那圈水波涟漪的颜色（用颜色字符串）。
> 
> 想要半透明就带上透明度，例如 "#66FF0000"。返回按钮自己，可链式。

- 参数 : color 颜色字符串，例如 "#66FF0000"
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").ripper("#66FF0000");
```


### ripper(color)

> 设置点按钮时那圈水波涟漪的颜色（用颜色整数）。
> 
> 用 $颜色 提供的 ARGB 颜色整数，例如 $颜色.红色。返回按钮自己，可链式。

- 参数 : color ARGB 颜色整数
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").ripper($颜色.红色);
```


### tip(tip)

> 设置长按这个按钮时弹出的提示文字。
> 
> Android 8.0 及以上用系统气泡提示，旧版本用 Toast。返回按钮自己，可链式。

- 参数 : tip 长按时显示的文字
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").tip("打开设置");
```


### bg(color)

> 设置按钮的背景颜色（用颜色字符串）。
> 
> 例如 "#FF222222"，半透明用 "#55222222"。返回按钮自己，可链式。

- 参数 : color 背景颜色字符串
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").bg("#FF222222");
```


### bg(color)

> 设置按钮的背景颜色（用颜色整数）。
> 
> 用 $颜色 提供的 ARGB 颜色整数，例如 $颜色.红色。返回按钮自己，可链式。

- 参数 : color ARGB 颜色整数
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").bg($颜色.红色);
```


### radius(radius)

> 把按钮四个角都设成同样的圆角大小。
> 
> 虽然方法名叫 radius，但它是圆角大小不是角度，单位是像素（不会按 dp 换算）。
> 数值越大角越圆，给很大数值就变成圆形按钮。返回按钮自己，可链式。

- 参数 : radius 圆角大小，单位像素
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").radius(12);
```


### icon(resName)

> 设置或换成按钮上显示的图标。
> 
> 传一个内置图标名或本地图片路径；找不到图就保持原来的图标不变。
> 返回按钮自己，可链式。

- 参数 : resName 内置图标名或本地图片路径
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_play_arrow");
item.icon("ic_stop");   //换成停止图标
```


### iconPadding(padding)

> 设置图标和按钮文字之间的间距（像素）。
> 
> 注意它调的是图标到文字的距离，不是图标到按钮边缘的距离。这些悬浮按钮本身没有文字，
> 所以改它一般看不出变化。返回按钮自己，可链式。

- 参数 : padding 图标与文字的间距，单位像素
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").iconPadding(8);
```


### iconSize(size)

> 设置按钮上图标的大小。
> 
> 单位是 dp，只改图标本身的大小，不会改变按钮整体尺寸。返回按钮自己，可链式。

- 参数 : size 图标大小，单位 dp
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").iconSize(30);
```


### cancelIconTint()

> 取消之前给图标染的颜色，让图标恢复成它本来的颜色。
> 
> 返回按钮自己，可链式。

- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").iconTint("#FF336699");
item.cancelIconTint();   //恢复图标原色
```


### iconTint(color)

> 给图标染一个颜色（用颜色字符串）。
> 
> 相当于给图标套一层单色滤镜。传 null 就清除染色、恢复图标原色。
> 返回按钮自己，可链式。

- 参数 : color 颜色字符串，传 null 清除染色
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").iconTint("#FF336699");
//item.iconTint(null);   //传 null 清除染色
```


### iconTint(color)

> 给图标染一个颜色（用颜色整数）。
> 
> 用 $颜色 提供的 ARGB 颜色整数。传 null 时保持当前染色不变，要清除请调 cancelIconTint()。
> 返回按钮自己，可链式。

- 参数 : color ARGB 颜色整数
- 返回 : 当前按钮自己，可继续链式设置
- 版本 : 1.0.0


```javascript
var item = $arc.item("ic_settings").iconTint($颜色.红色);
item.cancelIconTint();   //之后恢复原色
```


### getW()

> 读取这个按钮实际显示出来的宽度。
> 
> 单位像素。要等按钮真的显示出来、布局完之后再读，不然通常是 0。一般在点击回调里读。

- 返回 : 按钮宽度，单位像素


```javascript
var item = $arc.item("ic_settings");
item.click(function() {
    log("宽度=" + item.getW() + " px");
});
$arc.body("tools").add($arc.item("ic_menu")).add(item).show();
```


### getH()

> 读取这个按钮实际显示出来的高度。
> 
> 单位像素。要等按钮真的显示出来、布局完之后再读，不然通常是 0。

- 返回 : 按钮高度，单位像素


```javascript
var item = $arc.item("ic_settings");
item.click(function() {
    log("高度=" + item.getH() + " px");
});
$arc.body("tools").add($arc.item("ic_menu")).add(item).show();
```


