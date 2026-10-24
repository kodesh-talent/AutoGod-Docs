# 综合案例

- 更新时间:2026-10-22 10:58:41



使用脚本创建界面


```html
// 将布局文字保存在字符串中；每一行用加号连接，符合 ES5 语法。
// 中英文示例任选一套运行。图片资源需提前放到布局所写的路径。
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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="加载"
                title="Load" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--概览-->
                <text gravity="center" h="50" selectable="true" text="概览" />
                <load id="mLoad" show="false" />
                <button id="mButton" text="开始加载" />
                <!--设置主题颜色-->
                <text gravity="center" h="50" selectable="true" text="设置主题颜色 color=颜色" />
                <linear dir="h" w="max">
                    <load color="#57965C" marginEnd="15" />
                    <load color="#3574F0" marginEnd="15" />
                    <load color="#C94F4F" />
                </linear>
                <!--设置颜色组合-->
                <text gravity="center" h="50" selectable="true"
                    text="设置颜色组合 colors=颜色1,颜色2..." />
                <load colors="#57965C,#3574F0,#C94F4F,#FFC31F,#F501F5" />
                <!--设置尺寸-->
                <text gravity="center" h="50" selectable="true" text="设置尺寸 size=尺寸" />
                <linear dir="h" w="max">
                    <load marginEnd="15" size="20" />
                    <load marginEnd="15" size="25" />
                    <load size="30" />
                </linear>
                <!--设置显示于隐藏-->
                <text gravity="center" h="50" selectable="true" text="设置显示于隐藏 show=true" />
                <linear dir="h" w="max">
                    <load color="#57965C" marginEnd="15" show="true" />
                    <!--第二个加载器被隐藏了，所以实际上只能看到两个加载器-->
                    <load color="#3574F0" marginEnd="15" show="false" />
                    <load color="#C94F4F" />
                </linear>
                <text gravity="center" h="50" selectable="true"
                    text="第二个(蓝色的)加载器被隐藏了，所以实际上只能看到两个加载器" />
            </linear>
        </nested>
    </coord>
</ui>
`;
// 解析字符串得到界面对象，不需要另建布局文件。
var ui = $ui.layout(layout);
ui.id("mAppbar").back(function () {
    ui.finish();
});
// 这个示例只演示显示状态，不执行真实下载或网络请求。
var visible = false;
var loader = ui.id("mLoad");
ui.id("mButton").click(function () {
    visible = !visible;
    if (visible) {
        loader.show();
    } else {
        loader.hide();
    }
});
// 绑定好事件后再显示界面。
ui.show();
```


继续操作英文示例中创建的界面。
先运行上面的英文完整示例，再运行这里的代码；ui 是上面创建的界面对象，不要重新读取其他控件的布局文件。


```html
// 显示与隐藏只改变加载动画，不代表后台任务开始或完成。
var loader = ui.id("mLoad");
loader.hide();
// 本页的按钮回调会切换动画，学习时不需要等待或休眠。
```


