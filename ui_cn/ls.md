# 列表

- 更新时间:2026-10-22 10:58:41

> 列表-ls
> 
> 原生类型:{androidx.recyclerview.widget.RecyclerView}





<div style="width: 100%; position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe 
    src="//player.bilibili.com/player.html?isOutside=true&aid=116225355027820&bvid=BV12EwszPEux&cid=36684696067&p=1" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;"
    scrolling="no" 
    frameborder="no" 
    allowfullscreen="true">
  </iframe>
</div>

列表控件，算的算是一个比较复杂的控件，但是该组件确是最常用的组件之一，
因为它可以用来展示一个列表，比如一个商品列表、一个用户列表、一个消息列表等等。


![](./img/1036371318861000.png)

### 布局 - 子项布局

> 设置子项布局


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态栏 />
    <列表 高="最大" 标识="mLs" 外边距="15" 宽="最大">
        <!-- 列表布局中:用来指定每个子项目的布局 -->
        <布局 宽="最大">
            <!-- 卡片布局:需要配合线性布局来写更好看的界面 -->
            <卡片 外边距="2" 宽="最大">
                <线性布局 方向="横向" 重力="中|left" 内边距="15" 宽="最大">
                    <!-- 这里才是真正显示数据的地方 -->
                    <文字 标识="name" 最小宽度="120" />
                    <文字 标识="age" />
                    <线性布局 重力="中|右" 宽="最大" 权重="1">
                        <按钮 风格="文本" 标识="delBut" 文本="删除" 文本颜色="红色" />
                    </线性布局>
                </线性布局>
            </卡片>
        </布局>
    </列表>
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/1036371318861000.png)

列表数据绑定示例。请先执行上一段中文布局示例，再接着执行本段；沿用上一段的界面对象。

列表中的布局只规定每行有哪些控件；绑定回调负责把每条数据填到那一行里。
每次行视图创建或复用时，回调会收到 XLsHolder 行对象、Object 行数据和 int 行下标。
回调没有返回值。不要保存行对象供以后使用，因为滚动后同一行视图可能显示另一条数据。


```html
// 上一段布局中的列表标识为 mLs。
var 列表 = 界面.找控件("mLs");
// 先登记填充方法，再传入数据。
列表.绑定持有者(function (子布局, 数据, 位置) {
    子布局.找控件("name").设置文本("姓名：" + 数据.姓名);
    子布局.找控件("age").设置文本("年龄：" + 数据.年龄);
    // 示例只演示显示数据，隐藏模板里暂未使用的删除按钮。
    子布局.找控件("delBut").设置可见性(8);
});
列表.刷新([{姓名: "张三", 年龄: 16}, {姓名: "李四", 年龄: 18}]);
```


### 列数 - 列数

> 设置列数
> 
> 当该属性被设置的时候，布局将采用网格布局来添加子项。


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态栏 />
    <列表 高="最大" 标识="mLs" 外边距="15" 列数="2" 宽="最大">
        <!-- 列表布局中:用来指定每个子项目的布局 -->
        <布局 宽="最大">
            <!-- 卡片布局:需要配合线性布局来写更好看的界面 -->
            <卡片 外边距="2" 宽="最大">
                <线性布局 方向="横向" 重力="中|left" 内边距="15" 宽="最大">
                    <!-- 这里才是真正显示数据的地方 -->
                    <文字 标识="name" 最小宽度="120" />
                    <文字 标识="age" />
                    <线性布局 重力="中|右" 宽="最大" 权重="1">
                        <按钮 风格="文本" 标识="delBut" 文本="删除" 文本颜色="红色" />
                    </线性布局>
                </线性布局>
            </卡片>
        </布局>
    </列表>
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/1036885281225000.png)

### 内边距 - 内边距

> 设置内边距


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态栏 />
    <列表 高="最大" 标识="mLs" 内边距="50" 宽="最大">
        <!-- 列表布局中:用来指定每个子项目的布局 -->
        <布局 宽="最大">
            <!-- 卡片布局:需要配合线性布局来写更好看的界面 -->
            <卡片 外边距="2" 宽="最大">
                <线性布局 方向="横向" 重力="中|left" 内边距="15" 宽="最大">
                    <!-- 这里才是真正显示数据的地方 -->
                    <文字 标识="name" 最小宽度="120" />
                    <文字 标识="age" />
                    <线性布局 重力="中|右" 宽="最大" 权重="1">
                        <按钮 风格="文本" 标识="delBut" 文本="删除" 文本颜色="红色" />
                    </线性布局>
                </线性布局>
            </卡片>
        </布局>
    </列表>
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/1036952604432100.png)

### 背景颜色 - 背景颜色

> 设置背景颜色


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
var 布局内容 = `
<界面>
    <状态栏 />
    <列表 背景颜色="#1E1F22" 高="最大" 标识="mLs" 外边距="15" 宽="最大">
        <!-- 列表布局中:用来指定每个子项目的布局 -->
        <布局 宽="最大">
            <!-- 卡片布局:需要配合线性布局来写更好看的界面 -->
            <卡片 外边距="2" 宽="最大">
                <线性布局 方向="横向" 重力="中|left" 内边距="15" 宽="最大">
                    <!-- 这里才是真正显示数据的地方 -->
                    <文字 标识="name" 最小宽度="120" />
                    <文字 标识="age" />
                    <线性布局 重力="中|右" 宽="最大" 权重="1">
                        <按钮 风格="文本" 标识="delBut" 文本="删除" 文本颜色="红色" />
                    </线性布局>
                </线性布局>
            </卡片>
        </布局>
    </列表>
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/1037040261908500.png)

### 背景图片 - 背景图片

> 设置背景图片


```html
// 用字符串保存布局；标签表示控件，属性控制控件的外观或初始状态。
// 示例用到的本地资源需要提前准备，请把文件路径改为项目中的实际路径。
var 布局内容 = `
<界面>
    <状态栏 />
    <列表 外边距="30" 宽="最大" 标识="mLs" 背景图片="/res/bg-ls.png" 高="最大">
        <!-- 列表布局中:用来指定每个子项目的布局 -->
        <布局 宽="最大">
            <!-- 卡片布局:需要配合线性布局来写更好看的界面 -->
            <卡片 外边距="2" 宽="最大">
                <线性布局 内边距="15" 宽="最大" 方向="横向" 重力="中|left">
                    <!-- 这里才是真正显示数据的地方 -->
                    <文字 最小宽度="120" 标识="name" />
                    <文字 标识="age" />
                    <线性布局 宽="最大" 权重="1" 重力="中|右">
                        <按钮 文本="删除" 文本颜色="红色" 标识="delBut" 风格="文本" />
                    </线性布局>
                </线性布局>
            </卡片>
        </布局>
    </列表>
</界面>
`;
// 解析布局得到界面对象，再显示界面。
var 界面 = $界面.解析布局(布局内容);
界面.显示();
```


![](./img/1037283848936000.png)

### 滚动到顶部()

> “滚动到顶部”是 scrollTop 的中文名字：让列表平滑滚回第 0 项。


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙", "丙"]);
ls.滚动到顶部(); //滚回最上面
```


### 滚动到底部()

> “滚动到底部”是 scrollBottom 的中文名字：让列表平滑滚到最后一项。


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙", "丙", "丁"]);
ls.滚动到底部(); //滚到最后一项
```


### 滚动(位置)

> “滚动”是 scroll 的中文名字：让列表平滑滚到指定下标的那一项。
> 
> 下标从 0 开始：传 0 就是第一项。

- 参数 : 位置 {Number} 要滚动到的下标，从 0 开始


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
var arr = [];
for (var i = 0; i < 20; i++) {
    arr.push("第" + (i + 1) + "项");
}
ls.flush(arr);
ls.滚动(9); //滚到第 10 项
```


### 绑定持有者(持有者)

> “绑定持有者”是 bindHolder 的中文名字：告诉列表每一行该怎么把数据填到子控件上，必须在刷新数据前调用。
> 
> 回调函数收到三个参数：该行的界面对象、该行的数据、该行的下标（从 0 开始）。

- 参数 : 持有者 {function} 绑定回调，参数依次为该行界面对象、该行数据、该行下标


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><linear dir="h" padding="15"><text id="name" minW="120"/><text id="age"/></linear></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.绑定持有者(function(itemUi, itemData, position) {
    itemUi.id("name").setText("姓名:" + itemData.name);
    itemUi.id("age").setText("年龄:" + itemData.age);
});
ls.flush([{name: "张三", age: 16}, {name: "李四", age: 18}]);
```


### 刷新(数据)

> “刷新”是 flush 的中文名字：一次性设置整个列表的数据并立刻重绘。

- 参数 : 数据 {Array} 要显示的数据数组


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.刷新(["苹果", "香蕉", "橙子"]); //塞三条数据
```


### 刷新(数据, 位置)

> “刷新（单个）”是 flush(data, position) 的中文名字：只替换某一行的数据，其它行不动。

- 参数 : 数据 {Object} 新的数据
- 参数 : 位置 {Number} 要替换的那一行的下标，从 0 开始


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["苹果", "香蕉", "橙子"]);
ls.刷新("西瓜", 1); //把第二条换成西瓜
```


### 移除(位置)

> “移除”是 del 的中文名字：删掉指定下标的那一行，并自动刷新列表。

- 参数 : 位置 {Number} 要删除的那一行的下标，从 0 开始


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙", "丙"]);
ls.移除(0); //删掉第一条
```


### 添加(数据)

> “添加”是 add 的中文名字：在列表末尾追加一条数据并刷新。

- 参数 : 数据 {Object} 要追加的数据


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙"]);
ls.添加("丙"); //末尾追加一条
```


### 添加(数据, 位置)

> “添加（到位置）”是 add(data, position) 的中文名字：在指定下标插入一条数据。

- 参数 : 数据 {Object} 要插入的数据
- 参数 : 位置 {Number} 插入位置的下标，从 0 开始


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙", "丙"]);
ls.添加("新", 1); //插到第二条前面
```


### 清空()

> “清空”是 clear 的中文名字：把列表里所有数据删掉，列表变空白。


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙", "丙"]);
ls.清空(); //全部清空
```


### 获取数据()

> “获取数据”是 getData 的中文名字：读出列表当前的全部数据，返回一个数组。

- 返回 : {Array} 列表当前的数据数组
- 版本 : 1.7.3


```javascript
var ui = $ui.layout('<ui><statusbar/><ls id="mLs" w="max" h="max"><layout w="max"><text id="name" padding="15"/></layout></ls></ui>');
ui.show(); //把界面显示出来
var ls = ui.id("mLs"); //根据 id 拿到这个列表
ls.bindHolder(function(itemUi, itemData, position) {
    itemUi.id("name").setText(itemData);
});
ls.flush(["甲", "乙", "丙"]);
var data = ls.获取数据(); //读出全部数据
log("现在共有" + data.length + "条");
```


