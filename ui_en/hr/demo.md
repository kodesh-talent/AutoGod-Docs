# 综合案例

- 更新时间:2026-10-22 10:58:40



## 布局与脚本完整示例


```html
// 中英文版本任选一个运行；两段分别创建独立界面。
// 标签表示控件，属性改变外观；可以每次修改一个值，观察界面变化。
var layoutXml = `
<ui>
    <statusbar />
    <!--使用锚点布局配合滚动布局可以使应用条自带动画-->
    <coord w="max">
        <!--应用标题栏-->
        <appbar-layout w="max">
            <!--
            back:开启返回按钮
            scrollFlags:配置滚动布局滚动时的动画标记
            -->
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="分割线"
                title="Hr" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--概览-->
                <text gravity="center" h="50" selectable="true" text="概览" />
                <hr color="#C94F4F" margin="5" />
                <hr color="#57965C" margin="5" />
                <hr color="#3574F0" margin="5" />
                <!--设置颜色-->
                <text gravity="center" h="50" selectable="true" text="设置颜色 color=颜色" />
                <hr color="#C94F4F" />
                <!--设置尺寸-->
                <text gravity="center" h="50" selectable="true" text="设置尺寸 size=尺寸" />
                <!--允许设置小数，达到最小的尺寸 size=0.1 -->
                <hr margin="5" size="0.1" />
                <hr margin="5" size="1" />
                <hr margin="5" size="5" />
                <hr margin="5" size="10" />
                <!--设置开始边距-->
                <text gravity="center" h="50" selectable="true" text="设置开始边距 start=边距" />
                <hr start="100" />
                <!--设置结束边距-->
                <text gravity="center" h="50" selectable="true" text="设置结束边距 end=边距" />
                <hr end="100" />
            </linear>
        </nested>
    </coord>
</ui>
`;
var ui = $ui.layout(layoutXml);
// 按布局中的 id 取得应用条，点击返回按钮时结束当前界面。
ui.id("mAppbar").back(function () {
    ui.finish();
});
ui.show(); // 完成事件绑定后显示界面。
```


