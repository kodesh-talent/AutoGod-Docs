# 综合案例

- 更新时间:2026-10-22 10:58:42



使用脚本创建界面


```html
// 中英文示例任选一套运行；布局中的本地图片需要提前准备。
// 布局是普通字符串，逐行连接，不使用 ES6 模板字符串。
var layout = `
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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="范围条"
                title="Range" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--设置开始值-->
                <text gravity="center" h="50" selectable="true" text="设置开始值 form=数字" />
                <range id="demoRange" from="0" to="100" w="max" />
                <!--设置开始值-->
                <text gravity="center" h="50" selectable="true" text="设置开始值 fromValue=数字" />
                <range from="0" fromValue="10" to="100" w="max" />
                <range from="0" fromValue="20" to="100" w="max" />
                <!--设置结束值-->
                <text gravity="center" h="50" selectable="true" text="设置结束值 toValue=数字" />
                <range from="0" fromValue="10" to="100" toValue="50" w="max" />
                <range from="0" fromValue="20" to="100" toValue="50" w="max" />
                <!--设置进步值-->
                <text gravity="center" h="50" selectable="true" text="设置进步值 step=数字" />
                <range from="0" fromValue="10" step="1" to="100" toValue="50" w="max" />
                <!--设置主题颜色-->
                <text gravity="center" h="50" selectable="true" text="设置主题颜色 color=颜色" />
                <range color="#57965C" from="0" fromValue="10" to="100" toValue="50" w="max" />
                <range color="#C94F4F" from="0" fromValue="10" to="100" toValue="50" w="max" />
                <range color="#3574F0" from="0" fromValue="10" to="100" toValue="50" w="max" />
                <!--设置标签文字-->
                <text gravity="center" h="50" selectable="true" text="设置标签文字 label=文本" />
                <range label="比例:" w="max" />
                <!--设置标签后缀-->
                <text gravity="center" h="50" selectable="true" text="设置标签后缀 labelEnd=文本" />
                <range labelEnd="%" w="max" />
                <!--设置背景颜色-->
                <text gravity="center" h="50" selectable="true" text="设置背景颜色 bg=颜色" />
                <range bg="#57965C" w="max" />
                <range bg="#C94F4F" w="max" />
                <range bg="#3574F0" w="max" />
                <!--设置背景图片-->
                <text gravity="center" h="50" selectable="true"
                    text="设置背景图片 bgImg=图片路径" />
                <range bgImg="example/$ui - 交互界面/19.range-范围条/img/img.png" w="max" />
            </linear>
        </nested>
    </coord>
</ui>
`;
// 直接解析布局字符串，无需另建布局文件。
var ui = $ui.layout(layout);
// 按布局中的真实标识查找应用条，返回按钮用于关闭当前界面。
ui.id("mAppbar").back(function () {
    ui.finish();
});
// 回调收到两个数值，依次表示左端和右端的当前选择。
// 开始拖动、停止拖动及数值变化均可能触发回调，不要假定只调用一次。
ui.id("demoRange").onChange(function (from, to) {
    log("当前范围：" + from + " 至 " + to);
});
// 事件设置完毕后显示界面。
ui.show();
```


继续操作英文完整示例中已经创建的界面。
先运行英文示例，再运行这段代码，ui 是前面创建的界面对象。不要重新加载其他控件的布局文件。


```html
// 获取结果是 Java 列表，用 size() 获取数量、get(下标) 读取数值。
var values = ui.id("demoRange").getRange();
for (var i = 0; i < values.size(); i++) {
    log("端点 " + i + "：" + values.get(i));
}
```


