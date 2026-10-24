# 卡片布局

- 更新时间:2026-10-22 10:58:38

> 卡片布局-card
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法,但需要注意卡片布局本身是帧布局的子类，因此建议在卡片布局中加入线性布局来使用。
> 
> 原生类型:{com.google.android.material.card.MaterialCardView}




## 一、常用属性


### style - 风格

> 设置风格
> 
> 可选值:fill,outline,elevate


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <card style="outline" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### clickable - 是否可以点击

> 设置是否可以点击


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <card clickable="true" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### ripper - 涟漪颜色

> 设置涟漪颜色


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <card ripper="red" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### radius - 弧度

> 设置弧度
> 
> 单位:dp


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <card radius="10" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### minW - 最小宽度

> 设置最小宽度
> 
> 单位:dp


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <card minW="20" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### minH - 最小高度

> 设置最小高度
> 
> 单位:dp


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <card minH="20" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### bg - 背景颜色

> 设置背景颜色


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <card bg="#57965C" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### tint - 填充颜色

> 设置填充颜色
> 
> 背景颜色会无视卡片的圆弧角度，填充颜色会填充整个卡片，并且保证卡片的角度和样式


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <card tint="#57965C" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### bgImg - 背景图片

> 设置背景图片


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 示例引用的图片或子布局文件需要先放到项目中，并按实际位置修改路径。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <card bgImg="res/t01.png" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### padding - 内边距

> 设置内边距
> 
> 参数顺序:左,上,右,下(单位:dp)


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <card padding="0,0,0,0" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### gravity - 重力

> 设置重力
> 
> 卡片只能设置前景重力，不要求安卓版本。


```html
// 把布局写成字符串；引号内是控件名称和属性，修改属性值即可练习。
// 这里只演示容器属性；空容器可能不明显，可在容器内加入文本等子控件观察。
var layoutXml = `
<ui>
    <statusbar />
    <card gravity="center" />
</ui>
`;
// 解析字符串，得到管理这张界面的对象；接着显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


## 二、子控件属性表

被卡片布局包裹的子控件可以使用如下属性：

| 中文名   | 英文名        | 描述                                                         |
|----------|---------------|--------------------------------------------------------------|
| 布局方向 | dir           | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向 | resolveDir    | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽       | w             | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高       | h             | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 布局重力 | layout_gravity | 设置视图的布局重力，通过GravityAdd获取对应的重力值             |
| 外边距   | margin        | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距 | margin_left   | 单独设置视图的左外边距，单位为dp                             |
| 上外边距 | margin_top    | 单独设置视图的上外边距，单位为dp                             |
| 右外边距 | margin_right  | 单独设置视图的右外边距，单位为dp                             |
| 下外边距 | margin_bottom | 单独设置视图的下外边距，单位为dp                             |


## 三、常用函数


### setClickable(clickable)

> 设置可点击

- 参数 : clickable {boolean} 是否可点击
- 版本 : 1.8.2


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var card = ui.id("mCard");
//设置可点击
card.setClickable(true);
```


### setRipper(colorStr)

> 设置涟漪色

- 参数 : colorStr {string} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var card = ui.id("mCard");
//设置涟漪色
card.setRipper("#FF0000");
```


### setRipper(colorVal)

> 设置涟漪色

- 参数 : colorVal {int} 颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var card = ui.id("mCard");
//设置涟漪色
card.setRipper($color.RED);
```


### setBg(color)

> 设置背景颜色

- 参数 : color {int} 颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var card = ui.id("mCard");
//设置背景颜色
card.setBg($color.RED);
```


### setBg(color)

> 设置背景颜色

- 参数 : color {string} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var card = ui.id("mCard");
//设置背景颜色
card.setBg("#1E1F22");
```


### setTint(colorVal)

> 设置填充色

- 参数 : colorVal {int} 颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var card = ui.id("mCard");
//设置填充色
card.setTint($color.RED);
```


### setTint(colorStr)

> 设置填充色

- 参数 : colorStr {string} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var card = ui.id("mCard");
//设置填充色
card.setTint("#FF0000");
```


### setRadius(number)

> 设置弧度

- 参数 : number {float} 弧度(单位:dp)
- 版本 : 1.8.2


```javascript
//解析布局,获得ui对象
var ui = $ui.layout("./mUi.xml");
//获取控件
var card = ui.id("mCard");
//设置弧度
card.setRadius(15);
```


## 子控件属性表

被帧布局包裹的子控件可以使用如下属性：

| 中文名     | 英文名          | 描述                                                         |
|------------|-----------------|--------------------------------------------------------------|
| 布局方向   | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向   | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽         | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高         | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 布局重力   | layout_gravity  | 设置视图的布局重力，通过GravityAdd获取对应的重力值             |
| 外边距     | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距   | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距   | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距   | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距   | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |


