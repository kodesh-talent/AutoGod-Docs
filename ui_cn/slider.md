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


### 开始值 - 开始值

> 设置开始值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var 布局内容 = `
<界面>
    <状态条 />
    <滑动条 开始值="0" />
</界面>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/slider_from.png)

### 结束值 - 结束值

> 设置结束值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var 布局内容 = `
<界面>
    <状态条 />
    <滑动条 结束值="100" />
</界面>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/slider_to.png)

### 当前值 - 初始值

> 设置初始值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var 布局内容 = `
<界面>
    <状态条 />
    <滑动条 当前值="30" />
</界面>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/slider_value.png)

### 进步值 - 进步值

> 设置进步值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var 布局内容 = `
<界面>
    <状态条 />
    <滑动条 进步值="1" />
</界面>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/slider_step.png)

### 主题颜色 - 主题颜色

> 设置主题颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var 布局内容 = `
<界面>
    <状态条 />
    <滑动条 主题颜色="#FF0000" />
</界面>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/slider_demo.png)

### 标签 - 标签文字

> 设置标签文字


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var 布局内容 = `
<界面>
    <状态条 />
    <滑动条 标签="进度:" />
</界面>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/slider_label.png)

### 标签尾部 - 标签文字尾部

> 设置标签文字尾部


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var 布局内容 = `
<界面>
    <状态条 />
    <滑动条 标签尾部="个" />
</界面>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/slider_labelEnd.png)

### 内边距 - 内边距

> 设置内边距
> 
> 参数顺序:左,上,右,下(单位:dp)


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var 布局内容 = `
<界面>
    <状态条 />
    <滑动条 内边距="20,20,20,20" />
</界面>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/slider_padding.png)

### 背景颜色 - 背景颜色

> 设置背景颜色


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var 布局内容 = `
<界面>
    <状态条 />
    <滑动条 背景颜色="#1E1F22" />
</界面>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/slider_bg.png)

### 背景图片 - 背景图片

> 设置背景图片


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
// 若布局引用图片、视频或其他资源，请先准备文件并改成实际可用的路径。
var 布局内容 = `
<界面>
    <状态条 />
    <滑动条 背景图片="./资源/图片.png" />
</界面>
`;
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/slider_bgImg.png)

### 存储关键字 - 应用内存储

> 应用内存储
> 
> 通过storeKey(存储关键字)指定一个存储整数的关键字，获取值时可以直接通过$storage($存储)获取进度值。
> 
> 注意：不同的控件存储的类型不同，对于本控件(进度条)则存储的是整数类型，表达当前进度值


```html
// 将布局保存为字符串；标签表示控件，标签中的属性决定显示效果。
var 布局内容 =
    "<!-- 你必须在ui(界面)节点中通过store(存储)指定$storage($存储)的命名空间，等价于使用代码：var storage = $storage.create(\"MySlider\"); -->\n" +
    "<界面 存储=\"MySlider\">\n" +
    "    <状态栏 />\n" +
    "    <!-- 使用storeKey(存储关键字)属性，指定关键字，等价于使用代码：var data = $storage.create(\"MySlider\").getFloat(\"进度\"); -->\n" +
    "    <!-- 使用storeDef(存储默认值)属性，指定关键字，等价于使用代码：var data = $storage.create(\"MySlider\").getFloat(\"进度\",50); -->\n" +
    "    <滑动条 存储关键字=\"进度\" 存储默认值=\"50\" />\n" +
    "</界面>";
// 解析布局后得到界面对象，显示它即可查看本节属性的效果。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
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


### 设置背景颜色(颜色)

> “设置背景颜色”是 setBg 的中文名字（颜色数字版）：把整个滑动条背景涂成指定颜色。

- 参数 : 颜色 {Number} 颜色数字，例如 $color.RED
- 版本 : 1.8.2


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.设置背景颜色($color.RED); //背景涂成红色
```


### 设置背景颜色(颜色)

> “设置背景颜色”是 setBg 的中文名字（颜色字符串版）：把整个滑动条背景涂成指定颜色。

- 参数 : 颜色 {String} 颜色字符串，例如 "#FF0000"
- 版本 : 1.8.2


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.设置背景颜色("#FF0000"); //背景涂成红色
```


### 设置主题颜色(颜色)

> “设置主题颜色”是 setColor 的中文名字（颜色数字版）：换小圆点和已拖线段的颜色。

- 参数 : 颜色 {Number} 颜色数字，例如 $color.BLUE
- 版本 : 1.8.2


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.设置主题颜色($color.BLUE); //主题色变蓝
```


### 设置主题颜色(颜色)

> “设置主题颜色”是 setColor 的中文名字（颜色字符串版）：换小圆点和已拖线段的颜色。

- 参数 : 颜色 {String} 颜色字符串，例如 "#3574F0"
- 版本 : 1.8.2


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.设置主题颜色("#3574F0"); //主题色变蓝
```


### 标签格式化(回调)

> “标签格式化”是 onLabel 的中文名字：自定义拖动时弹出小标签上显示的文字。

- 参数 : 回调 {function} 格式化函数，参数是当前数值，返回要显示的文字


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.标签格式化(function(value) {
    return "评分 " + value;
});
```


### 监听变化(回调)

> “监听变化”是 onChange 的中文名字：用户拖动时回调，并告诉你当前数值。

- 参数 : 回调 {function} 变化回调，参数是当前数值；传 null 取消监听


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.监听变化(function(value) {
    log("当前值:" + value);
});
```


### 获取值()

> “获取值”是 getValue 的中文名字：读出小圆点当前停在多少。

- 返回 : {number} 当前数值


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.setValue(50);
var val = slider.获取值();
log("当前是" + val);
```


### 设置值(数值)

> “设置值”是 setValue 的中文名字：代码里直接把小圆点跳到某个数值。

- 参数 : 数值 {Number} 要设的数值


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.设置值(50); //小圆点跳到 50
```


### 设置开始值(开始值)

> “设置开始值”是 setFrom 的中文名字：代码里设滑动条最左边允许到几。

- 参数 : 开始值 {Number} 最小值


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.设置开始值(10); //最左边变成 10
```


### 设置进步值(进步值)

> “设置进步值”是 setStep 的中文名字：设每次拖动跳几格。

- 参数 : 进步值 {Number} 步长


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.设置进步值(5); //每次跳 5
```


### 设置结束值(结束值)

> “设置结束值”是 setTo 的中文名字：代码里设滑动条最右边允许到几。

- 参数 : 结束值 {Number} 最大值


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.设置结束值(200); //最右边变成 200
```


### 设置数据(开始, 结束)

> “设置数据”是 setData 的中文名字（两参数版）：一次性设最小值和最大值。

- 参数 : 开始 {Number} 最小值
- 参数 : 结束 {Number} 最大值，必须比开始大


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.设置数据(10, 90); //最小 10，最大 90
```


### 设置数据(开始, 结束, 当前值)

> “设置数据”是 setData 的中文名字（三参数版）：设最小、最大，并直接把小圆点放到当前值。

- 参数 : 开始 {Number} 最小值
- 参数 : 结束 {Number} 最大值，必须比开始大
- 参数 : 当前值 {Number} 小圆点当前位置


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.设置数据(10, 90, 30); //最小 10，最大 90，小圆点停在 30
```


### 监听触摸开始(回调)

> “监听触摸开始”是 onTouchStart 的中文名字：用户刚按住滑动条时回调。

- 参数 : 回调 {function} 手指按下时回调，无参数；传 null 取消
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.监听触摸开始(function() {
    log("开始拖了");
});
```


### 监听触摸结束(回调)

> “监听触摸结束”是 onTouchStop 的中文名字：用户松手时回调。

- 参数 : 回调 {function} 手指松开时回调，无参数；传 null 取消
- 版本 : 1.9.5


```javascript
var ui = $ui.layout('<ui><statusbar/><slider id="mSlider" w="max"/></ui>');
ui.show(); //把界面显示出来
var slider = ui.id("mSlider"); //根据 id 拿到这个滑动条
slider.监听触摸结束(function() {
    log("松手了");
});
```


