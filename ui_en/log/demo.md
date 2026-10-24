# 综合案例

- 更新时间:2026-10-22 10:58:41



## Xml代码


```javascript
// 将布局内容作为字符串传入解析方法；返回值是可查找控件的界面对象。
var layout =
    "<ui>\n" +
    "    <statusbar />\n" +
    "    <!--使用锚点布局配合滚动布局可以使应用条自带动画-->\n" +
    "    <coord w=\"max\">\n" +
    "        <!--应用标题栏-->\n" +
    "        <appbar-layout w=\"max\">\n" +
    "            <!--\n" +
    "            back:开启返回按钮\n" +
    "            scrollFlags:配置滚动布局滚动时的动画标记\n" +
    "            -->\n" +
    "            <appbar back=\"true\" id=\"appbar\" scrollFlags=\"scroll|enterAlways\" subTitle=\"加载\"\n" +
    "                title=\"Load\" w=\"max\" />\n" +
    "        </appbar-layout>\n" +
    "        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->\n" +
    "        <nested behavior=\"appbar\" h=\"max\" w=\"max\">\n" +
    "            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->\n" +
    "            <!--padding:增加内边距[左,上,右,下]-->\n" +
    "            <linear h=\"max\" padding=\"20,20,20,100\" w=\"max\">\n" +
    "                <!--概览-->\n" +
    "                <text gravity=\"center\" h=\"50\" selectable=\"true\" text=\"概览\" />\n" +
    "                <load />\n" +
    "\n" +
    "                <!--设置主题颜色-->\n" +
    "                <text gravity=\"center\" h=\"50\" selectable=\"true\" text=\"设置主题颜色 color=颜色\" />\n" +
    "                <linear dir=\"h\" w=\"max\">\n" +
    "                    <load color=\"#57965C\" marginEnd=\"15\" />\n" +
    "                    <load color=\"#3574F0\" marginEnd=\"15\" />\n" +
    "                    <load color=\"#C94F4F\" />\n" +
    "                </linear>\n" +
    "\n" +
    "                <!--设置颜色组合-->\n" +
    "                <text gravity=\"center\" h=\"50\" selectable=\"true\"\n" +
    "                    text=\"设置颜色组合 colors=颜色1,颜色2...\" />\n" +
    "                <load colors=\"#57965C,#3574F0,#C94F4F\" />\n" +
    "\n" +
    "            </linear>\n" +
    "        </nested>\n" +
    "    </coord>\n" +
    "</ui>\n";
var ui = $ui.layout(layout);
```


