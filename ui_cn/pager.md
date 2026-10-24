# 多页布局

- 更新时间:2026-10-22 10:58:41

> 多页布局-pager
> 
> 多页布局允许用户在里面写多个界面并实现界面左右滑动，并且支持绑定标签页布局(tab)以及导航栏(nav)
> 
> 原生类型:{androidx.viewpager2.widget.ViewPager2}





<div style="width: 100%; position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe 
    src="//player.bilibili.com/player.html?isOutside=true&aid=116225439045460&bvid=BV1HbwsztEVD&cid=36685090615&p=1" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;"
    scrolling="no" 
    frameborder="no" 
    allowfullscreen="true">
  </iframe>
</div>

多页布局常常配合导航栏(nav)、标签布局(tab)来使用。


## 一、常用属性


### 布局 - 多页布局

> 设置多页布局
> 
> 其中每个'界面'最后都会被解析成一个布局，本质上就是个'线性布局'。


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态条 />
    <多页布局 宽="最大" 高="最大">
        <布局 />
        <布局 />
        <布局 />
    </多页布局>
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


### 默认下标 - 默认下标页面

> 设置默认下标页面


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态条 />
    <多页布局 默认下标="0" />
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


### 内边距 - 内边距

> 设置内边距


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态条 />
    <!--内边距顺序是:左,上,右,下-->
    <!--只设置一个值：则设置所有方向的内边距-->
    <!--只设置两个值：则设置左右和上下方向的内边距-->
    <多页布局 内边距="0,0,0,0" />
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


### 重力 - 重力

> 设置重力


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态条 />
    <多页布局 重力="开始" />
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


### 背景颜色 - 背景颜色

> 设置背景颜色


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态条 />
    <多页布局 背景颜色="#1E1F22" />
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


### 背景图片 - 背景图片

> 设置背景图片


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
// 示例用到的本地资源需要提前准备，请把文件路径改为项目中的实际路径。
var 布局内容 = `
<界面>
    <状态条 />
    <多页布局 背景图片="./资源/图片01.png" />
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


## 二、常用函数


### 设置下标(index)

> “设置下标”是 setCurIndex 的中文名字：让多页布局切到指定下标的那一页。

- 参数 : index {Number} 要切到的页下标，从 0 开始


```javascript
var ui = $ui.layout('<ui><statusbar/><pager id="mPager" w="max" h="max"><fragment><text text="第一页" gravity="center"/></fragment><fragment><text text="第二页" gravity="center"/></fragment></pager></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //根据 id 拿到这个多页布局
pager.设置下标(1); //切到第二页
```


### 获取下标()

> “获取下标”是 curIndex 的中文名字：读出当前停在哪一页，返回下标数字。

- 返回 : {Number} 当前页的下标，从 0 开始


```javascript
var ui = $ui.layout('<ui><statusbar/><pager id="mPager" w="max" h="max"><fragment><text text="第一页" gravity="center"/></fragment><fragment><text text="第二页" gravity="center"/></fragment></pager></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //根据 id 拿到这个多页布局
var now = pager.获取下标(); //读出当前页下标
log("现在在第" + (now + 1) + "页");
```


### 绑定(xTab)

> “绑定（标签栏）”是 bind(tab) 的中文名字：把多页布局和顶部标签栏联动起来。

- 参数 : xTab {XTab} 要联动的标签栏控件，用 ui.id("...") 拿到


```javascript
var ui = $ui.layout('<ui><statusbar/><linear dir="v" w="max" h="max"><tab id="mTab" h="50"><item text="首页"/><item text="我的"/></tab><pager id="mPager" w="max" h="max"><fragment><text text="首页内容" gravity="center"/></fragment><fragment><text text="我的内容" gravity="center"/></fragment></pager></linear></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //拿到多页布局
var tab = ui.id("mTab"); //拿到标签栏
pager.绑定(tab); //联动
```


### 绑定(xNav)

> “绑定（导航栏）”是 bind(nav) 的中文名字：把多页布局和底部导航栏联动起来。

- 参数 : xNav {XNav} 要联动的底部导航栏控件，用 ui.id("...") 拿到


```javascript
var ui = $ui.layout('<ui><statusbar/><linear dir="v" w="max" h="max" gravity="bottom"><pager id="mPager" w="max" h="max"><fragment><text text="主页" gravity="center"/></fragment><fragment><text text="设置" gravity="center"/></fragment></pager><nav id="mNav" w="max"><menu text="主页"/><menu text="设置"/></nav></linear></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //拿到多页布局
var nav = ui.id("mNav"); //拿到底部导航栏
pager.绑定(nav); //联动
```


### 监听界面切换(回调)

> “监听界面切换”是 onCheck 的中文名字：用户切到某一页时回调，并告诉你当前页下标。

- 参数 : 回调 {function} 切页回调，参数是当前页下标（从 0 开始）


```javascript
var ui = $ui.layout('<ui><statusbar/><pager id="mPager" w="max" h="max"><fragment><text text="第一页" gravity="center"/></fragment><fragment><text text="第二页" gravity="center"/></fragment></pager></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //拿到多页布局
pager.监听界面切换(function(index) {
    log("切到了第" + (index + 1) + "页");
});
```


### 监听状态改变(回调)

> “监听状态改变”是 onState 的中文名字：监听页面正在拖动、停住等滑动状态。

- 参数 : 回调 {function} 状态回调，参数为状态数字（0 停住 / 1 拖动 / 2 惯性滑动）


```javascript
var ui = $ui.layout('<ui><statusbar/><pager id="mPager" w="max" h="max"><fragment><text text="第一页" gravity="center"/></fragment><fragment><text text="第二页" gravity="center"/></fragment></pager></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //拿到多页布局
pager.监听状态改变(function(state) {
    if (state == 0) {
        log("滑动停住了");
    }
});
```


