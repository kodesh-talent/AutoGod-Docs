# 滑动条

- 更新时间:2026-10-22 10:58:42

> 滑动条-slider
> 
> 原生类型:{com.google.android.material.slider.Slider}





<div style="width: 100%; position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe 
    src="//player.bilibili.com/player.html?isOutside=true&aid=116230673406058&bvid=BV18jwKzXEKu&cid=36706649433&p=1" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;"
    scrolling="no" 
    frameborder="no" 
    allowfullscreen="true">
  </iframe>
</div>

滚动条：常用于动态设置数字参数，通过滑动就可以变换数值。


![](./img/slider_demo.png)

## 一、常用属性


### from - 开始值

> 设置开始值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear w="max" h="max" dir="v" gravity="center">
        <!-- 滑动条 默认开始值是0 结束值是100 -->
        <slider  />
        <!-- 滑动条 设置开始值 from="20" -->
        <slider from="20" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/slider_from.png)

### to - 结束值

> 设置结束值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear w="max" h="max" dir="v" gravity="center">
        <!-- 滑动条 默认开始值是0 结束值是100 -->
        <slider  />
        <!-- 滑动条
        设置开始值 from="20"
        设置结束值 to="30"
        -->
        <slider from="20" to="30" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/slider_to.png)

### value - 初始值

> 设置初始值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear w="max" h="max" dir="v" gravity="center">
        <!-- 滑动条 默认开始值是0 结束值是100
        设置当前值为 50
        -->
        <slider value="50" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/slider_value.png)

### step - 进步值

> 设置进步值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear w="max" h="max" dir="v" gravity="center">
        <!-- 滑动条 默认开始值是0 结束值是100
        设置进步值为 1
        -->
        <slider step="1" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/slider_step.png)

### color - 主题颜色

> 设置主题颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear w="max" h="max" dir="v" gravity="center">
        <!-- 滑动条 设置主题颜色 color="#518855" -->
        <slider />
        <slider color="#518855" />
        <slider color="#B44A4A" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/slider_demo.png)

### label - 标签文字

> 设置标签文字


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear w="max" h="max" dir="v" gravity="center">
        <!-- 滑动条 默认开始值是0 结束值是100
        设置标签 label="进度:"
        -->
        <slider label="进度:" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/slider_label.png)

### labelEnd - 标签文字尾部

> 设置标签文字尾部


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear w="max" h="max" dir="v" gravity="center">
        <!-- 滑动条 默认开始值是0 结束值是100
        设置尾部标签 labelEnd="个"
        注意：label和labelEnd只能有一个生效，避免重复设置
        -->
        <slider labelEnd="个" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/slider_labelEnd.png)

### padding - 内边距

> 设置内边距


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear w="max" h="max" dir="v" gravity="center">
        <!-- 滑动条 默认开始值是0 结束值是100 -->
        <!--padding顺序是:左,上,右,下-->
        <!--padding只设置一个值：则设置所有方向的内边距-->
        <!--padding只设置两个值：则设置左右和上下方向的内边距-->
        <slider padding="5" />
        <slider padding="10" />
        <slider padding="15" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/slider_padding.png)

### bg - 背景颜色

> 设置背景颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<ui>
    <statusbar />
    <linear w="max" h="max" dir="v" gravity="center">
        <!-- 滑动条 默认开始值是0 结束值是100
        设置背景颜色 bg="#518855"
        -->
        <slider bg="#518855" />
        <slider bg="#B44A4A" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/slider_bg.png)

### bgImg - 背景图片

> 设置背景图片


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
// 若布局引用图片、视频或其他资源，请先准备文件并改成实际可用的路径。
var layoutXml = `
<ui>
    <statusbar />
    <linear w="max" h="max" dir="v" gravity="center">
        <!-- 滑动条 默认开始值是0 结束值是100
        设置背景图片 bgImg="/res/bg_slider.png"
        -->
        <slider bgImg="/res/bg_slider.png" />
    </linear>
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


![](./img/slider_bgImg.png)

### storeKey - 应用内存储

> 应用内存储
> 
> 通过storeKey(存储关键字)指定一个存储整数的关键字，获取值时可以直接通过$storage($存储)获取进度值。
> 
> 注意：不同的控件存储的类型不同，对于本控件(进度条)则存储的是整数类型，表达当前进度值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var layoutXml = `
<!-- 你必须在ui(界面)节点中通过store(存储)指定$storage($存储)的命名空间，等价于使用代码：var storage = $storage.create("MySlider"); -->
<ui store="MySlider">
    <statusbar />
    <!-- 使用storeKey(存储关键字)属性，指定关键字，等价于使用代码：var data = $storage.create("MySlider").getFloat("progress"); -->
    <!-- 使用storeDef(存储默认值)属性，指定关键字，等价于使用代码：var data = $storage.create("MySlider").getFloat("progress",50); -->
    <slider storeKey="progress" storeDef="50" />
</ui>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var ui = $ui.layout(layoutXml);
ui.show();
```


如果我们已经配置好了应用内存储，则可以直接获取数据：

注意：一、要使用应用内存储，必须在ui(界面)节点指定属性store(存储)的值，该值指定存储的命名空间；
二、不是所有的控件都支持应用内存储；
三、不同的控件存储的数据类型可能都不一致，例如：输入类型的控件存储的是字符串类型，开关、多选框存储的就是布尔类型的数据。


```javascript
//创建(或者加载)存储对象
var storage = $storage.create("MySlider");//名称要一致
//获取数据
var data = storage.getFloat("progress",50);//数据类型是小数
```


## 二、常用函数


### setBg(color)

> 代码里把整个滑动条的背景涂成指定颜色（用颜色数字）。

- 参数 : color {Number} 颜色数字，例如 $color.RED
- 版本 : 1.8.2


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setBg($color.RED); //背景涂成红色
```


### setBg(color)

> 代码里把整个滑动条的背景涂成指定颜色（用颜色字符串，如 "#FF0000"）。

- 参数 : color {String} 颜色字符串，例如 "#FF0000"
- 版本 : 1.8.2


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setBg("#FF0000"); //背景涂成红色
```


### setColor(color)

> 代码里把滑动条的主题色（小圆点、已拖过的那一段线）换成指定颜色（颜色数字版）。

- 参数 : color {Number} 颜色数字，例如 $color.BLUE
- 版本 : 1.8.2


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setColor($color.BLUE); //主题色变蓝
```


### setColor(color)

> 代码里把滑动条的主题色换成指定颜色（颜色字符串版，如 "#3574F0"）。

- 参数 : color {String} 颜色字符串，例如 "#3574F0"
- 版本 : 1.8.2


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setColor("#3574F0"); //主题色变蓝
```


### onLabel(callback)

> 自定义拖动时弹出的那个小标签上显示什么字。
> 
> 你传一个函数，拖动到某个数值时系统会把当前数值传给你，你返回一段想显示的文字。返回 null 则显示原始数字。

- 参数 : callback {function} 格式化函数，参数是当前数值，返回要显示的文字


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.onLabel(function(value) {
    return "评分 " + value;
});
```


### onChange(callback)

> 监听用户拖动滑动条：小圆点一动就回调，并告诉你当前数值。
> 
> 注意：只监听用户手动拖出来的变化，代码里 setValue 不会触发。传 null 可取消监听。

- 参数 : callback {function} 变化回调，参数是当前数值；传 null 取消监听


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.onChange(function(value) {
    log("当前值:" + value);
});
```


### getValue()

> 读出小圆点当前停在多少。

- 返回 : {number} 当前数值


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setValue(50);
var val = slider.getValue(); //读出来
log("当前是" + val);
```


### setValue(value)

> 代码里直接把小圆点跳到某个数值。

- 参数 : value {Number} 要设的数值


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setValue(50); //小圆点跳到 50
```


### setFrom(from)

> 代码里设置滑动条允许的最小值（最左边是几）。

- 参数 : from {Number} 最小值


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setFrom(10); //最左边变成 10
```


### setStep(step)

> 设置每次拖动要跳几格（步长）。比如步长 5，小圆点就只能停在 0、5、10、15…

- 参数 : step {Number} 步长


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setStep(5); //每次跳 5
```


### setTo(to)

> 代码里设置滑动条允许的最大值（最右边是几）。

- 参数 : to {Number} 最大值


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setTo(200); //最右边变成 200
```


### setData(from, to)

> 一次性设置滑动条的最小值、最大值（开始值和结束值）。结束值必须比开始值大。

- 参数 : from {Number} 最小值（开始）
- 参数 : to {Number} 最大值（结束），必须比 from 大


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setData(10, 90); //最小 10，最大 90
```


### setData(from, to, value)

> 一次性设置最小值、最大值，并把小圆点直接放到某个当前值。结束值必须比开始值大。

- 参数 : from {Number} 最小值（开始）
- 参数 : to {Number} 最大值（结束），必须比 from 大
- 参数 : value {Number} 小圆点当前位置


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setData(10, 90, 30); //最小 10，最大 90，小圆点停在 30
```


### onTouchStart(callback)

> 监听用户“刚用手指按住滑动条”这一刻，立刻回调你传进来的函数（没有参数）。
> 
> 传 null 可取消监听。

- 参数 : callback {function} 手指按下时回调，无参数；传 null 取消
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.onTouchStart(function() {
    log("开始拖了");
});
```


### onTouchStop(callback)

> 监听用户“手指离开滑动条”这一刻，立刻回调你传进来的函数（没有参数）。
> 
> 传 null 可取消监听。

- 参数 : callback {function} 手指松开时回调，无参数；传 null 取消
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.onTouchStop(function() {
    log("松手了");
});
```


