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


### fragment - 多页布局

> 设置多页布局
> 
> 其中每个fragment最后都会被解析成一个布局，把这个节点理解为ui节点就好了，本质上就是个LinearLayout。


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<ui>
    <statusbar />
    <pager w="max" h="max">
        <fragment />
        <fragment />
        <fragment />
    </pager>
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


### def - 默认下标页面

> 设置默认下标页面


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var layoutXml = `
<ui>
    <statusbar />
    <pager def="0" />
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
    <pager padding="20" />
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
    <pager gravity="start" />
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
    <radio bg="#1E1F22" />
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
    <pager bgImg="./img.png" />
</ui>
`;
// 解析布局得到界面对象，再显示界面。
var ui = $ui.layout(layoutXml);
ui.show();
```


## 二、常用函数


### setCurIndex(index)

> 让多页布局立刻切到指定下标的那一页。
> 
> 下标从 0 开始：传 0 就是第一页，传 1 就是第二页。

- 参数 : index {Number} 要切到的页下标，从 0 开始


```javascript
//先用一段 XML 创建界面：一个占满全屏的多页布局，里面有两页
var ui = $ui.layout('<ui><statusbar/><pager id="mPager" w="max" h="max"><fragment><text text="第一页" gravity="center"/></fragment><fragment><text text="第二页" gravity="center"/></fragment></pager></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //根据 id 拿到这个多页布局
pager.setCurIndex(1); //直接切到第二页
```


### curIndex()

> 读出用户当前正停在哪一页，返回一个下标数字（从 0 开始）。

- 返回 : {Number} 当前页的下标，从 0 开始


```javascript
var ui = $ui.layout('<ui><statusbar/><pager id="mPager" w="max" h="max"><fragment><text text="第一页" gravity="center"/></fragment><fragment><text text="第二页" gravity="center"/></fragment></pager></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //根据 id 拿到这个多页布局
var now = pager.curIndex(); //读出当前是第几页
log("现在在第" + (now + 1) + "页");
```


### bind(xTab)

> 把多页布局和顶部标签栏（tab）绑在一起：左右滑页时标签跟着高亮，点标签时页面跟着切。

- 参数 : xTab {XTab} 要联动的标签栏控件，用 ui.id("...") 拿到


```javascript
//先用一段 XML 创建界面：上面一个标签栏（两个 item），下面一个两页的多页布局
var ui = $ui.layout('<ui><statusbar/><linear dir="v" w="max" h="max"><tab id="mTab" h="50"><item text="首页"/><item text="我的"/></tab><pager id="mPager" w="max" h="max"><fragment><text text="首页内容" gravity="center"/></fragment><fragment><text text="我的内容" gravity="center"/></fragment></pager></linear></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //拿到多页布局
var tab = ui.id("mTab"); //拿到标签栏
pager.bind(tab); //绑上后，滑页和点标签会同步
```


### bind(xNav)

> 把多页布局和底部导航栏（nav）绑在一起：点底部导航切页，左右滑页时导航高亮跟着变。

- 参数 : xNav {XNav} 要联动的底部导航栏控件，用 ui.id("...") 拿到


```javascript
//先用一段 XML 创建界面：中间是多页布局，底部是导航栏
var ui = $ui.layout('<ui><statusbar/><linear dir="v" w="max" h="max" gravity="bottom"><pager id="mPager" w="max" h="max"><fragment><text text="主页" gravity="center"/></fragment><fragment><text text="设置" gravity="center"/></fragment></pager><nav id="mNav" w="max"><menu text="主页"/><menu text="设置"/></nav></linear></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //拿到多页布局
var nav = ui.id("mNav"); //拿到底部导航栏
pager.bind(nav); //绑上后，点导航和滑页会同步
```


### onCheck(callback)

> 监听用户切页：每当用户滑到（或点到）某一页时，就会回调你传进来的函数，并告诉你当前页下标。

- 参数 : callback {function} 切页回调，参数是当前页下标（从 0 开始）


```javascript
var ui = $ui.layout('<ui><statusbar/><pager id="mPager" w="max" h="max"><fragment><text text="第一页" gravity="center"/></fragment><fragment><text text="第二页" gravity="center"/></fragment></pager></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //拿到多页布局
//监听切页
pager.onCheck(function(index) {
    log("切到了第" + (index + 1) + "页");
});
```


### onState(callback)

> 监听页面滑动状态变化（正在滑、停住了、甩动中），一般用得较少。
> 
> 回调参数 state 是一个数字：0 表示已停止，1 表示正在拖动，2 表示正在惯性滑动。

- 参数 : callback {function} 状态回调，参数为状态数字（0 停住 / 1 拖动 / 2 惯性滑动）


```javascript
var ui = $ui.layout('<ui><statusbar/><pager id="mPager" w="max" h="max"><fragment><text text="第一页" gravity="center"/></fragment><fragment><text text="第二页" gravity="center"/></fragment></pager></ui>');
ui.show(); //把界面显示出来
var pager = ui.id("mPager"); //拿到多页布局
//监听滑动状态
pager.onState(function(state) {
    if (state == 0) {
        log("滑动停住了");
    }
});
```


