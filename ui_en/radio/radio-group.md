# 单选按钮组

- 更新时间:2026-10-22 10:58:42

> 单选按钮组-radio-group
> 
> 在此布局中，单选按钮会自动取消和选中，保证一组按钮只被选中一个
> 
> 是布局父类的(XLayout)的子类
> 
> 原生类型:{android.widget.RadioGroup}




## 一、常用属性


### dir - 排列方向

> 设置排列方向
> 
> 可选:v:竖向排列,h:横向排列


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<ui>
    <statusbar />
    <radio-group dir="h" />
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### color - 主题颜色

> 设置主题颜色


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<ui>
    <statusbar />
    <radio-group color="#57965C" text="主题色为绿色" />
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### padding - 内边距

> 设置内边距


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<ui>
    <statusbar />
    <!--padding顺序是:左,上,右,下-->
    <!--padding只设置一个值：则设置所有方向的内边距-->
    <!--padding只设置两个值：则设置左右和上下方向的内边距-->
    <radio-group padding="20" text="内边距" />
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### gravity - 重力

> 设置重力


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<ui>
    <statusbar />
    <radio-group gravity="start" h="100" margin="20" text="重力:start" w="max" />
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### bg - 背景颜色

> 设置背景颜色


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<ui>
    <statusbar />
    <radio-group bg="#1E1F22" text="背景颜色" />
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### bgImg - 背景图片

> 设置背景图片


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
// 示例用到的本地资源需要提前准备，请把文件路径改为项目中的实际路径。
var layoutXml = `
<ui>
    <statusbar />
    <radio-group bgImg="./img.png" text="背景图片" />
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### storeKey - 应用内存储

> 应用内存储
> 
> 通过storeKey(存储关键字)指定一个存储整数的关键字，获取值时可以直接通过$storage($存储)获取进度值。
> 
> 注意：不同的控件存储的类型不同，对于本控件(进度条)则存储的是整数类型，表达当前进度值


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<!-- 你必须在ui(界面)节点中通过store(存储)指定$storage($存储)的命名空间，等价于使用代码：var storage = $storage.create("MyRadioGroup"); -->
<ui store="MyRadioGroup">
    <statusbar />
    <!-- 使用storeKey(存储关键字)属性，指定关键字，等价于使用代码：var data = $storage.create("MyRadioGroup").getInt("index"); -->
    <!-- 使用storeDef(存储默认值)属性，指定关键字，等价于使用代码：var data = $storage.create("MyRadioGroup").getInt("index",0); -->
    <radio-group storeKey="index" storeDef="0">
        <radio text="吃饭"/>
        <radio text="睡觉"/>
        <radio text="游戏"/>
    </radio-group>
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


如果我们已经配置好了应用内存储，则可以直接获取数据：

注意：一、要使用应用内存储，必须在ui(界面)节点指定属性store(存储)的值，该值指定存储的命名空间；
二、不是所有的控件都支持应用内存储；
三、不同的控件存储的数据类型可能都不一致，例如：输入类型的控件存储的是字符串类型，开关、多选框存储的就是布尔类型的数据。


```javascript
//创建(或者加载)存储对象
var storage = $storage.create("MyRadioGroup");//名称要一致
//获取数据
var data = storage.getInt("index",0);//数据类型是整数
```


### check(index)

> 代码里主动选中组里第几个单选按钮（下标从 0 开始）。

- 参数 : index {Number} 要选中的按钮下标，从 0 开始


```javascript
//先用一段 XML 创建界面：一个单选按钮组，里面三个按钮
var ui = $ui.layout('<ui><statusbar/><radio-group id="mRg" w="max"><radio text="吃饭"/><radio text="睡觉"/><radio text="游戏"/></radio-group></ui>');
ui.show(); //把界面显示出来
var rg = ui.id("mRg"); //根据 id 拿到这个单选按钮组
rg.check(1); //默认选中第二个（睡觉）
```


### onCheck(callback)

> 监听用户在组里点了哪个按钮：一变就回调，并告诉你被选中按钮的下标（从 0 开始）。

- 参数 : callback {function} 选中回调，参数是被选中按钮的下标（从 0 开始）


```javascript
var ui = $ui.layout('<ui><statusbar/><radio-group id="mRg" w="max"><radio text="吃饭"/><radio text="睡觉"/><radio text="游戏"/></radio-group></ui>');
ui.show(); //把界面显示出来
var rg = ui.id("mRg"); //根据 id 拿到这个单选按钮组
//监听选中变化
rg.onCheck(function(index) {
    log("你选了第" + (index + 1) + "个");
});
```


### getCheckedIndex()

> 读出当前组里选中的是第几个按钮，返回下标（从 0 开始）。
> 
> 如果一个都没选，返回 -1。

- 返回 : {Number} 选中按钮的下标（从 0 开始）；一个都没选返回 -1


```javascript
var ui = $ui.layout('<ui><statusbar/><radio-group id="mRg" w="max"><radio text="吃饭"/><radio text="睡觉"/><radio text="游戏"/></radio-group></ui>');
ui.show(); //把界面显示出来
var rg = ui.id("mRg"); //根据 id 拿到这个单选按钮组
rg.check(2); //选中第三个
var i = rg.getCheckedIndex(); //读出下标
log("选中了第" + (i + 1) + "个");
```


### getCheckedText()

> 读出当前选中那个按钮上写的文字。
> 
> 如果一个都没选，返回 null。

- 返回 : {String} 选中按钮的文字；一个都没选返回 null


```javascript
var ui = $ui.layout('<ui><statusbar/><radio-group id="mRg" w="max"><radio text="吃饭"/><radio text="睡觉"/><radio text="游戏"/></radio-group></ui>');
ui.show(); //把界面显示出来
var rg = ui.id("mRg"); //根据 id 拿到这个单选按钮组
rg.check(1); //选中第二个
var t = rg.getCheckedText(); //读出文字
log("你选了:" + t); //输出 睡觉
```


