# 综合案例

- 更新时间:2026-10-22 10:58:40



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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="悬浮按钮"
                title="Fab" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--概览-->
                <text gravity="center" h="50" selectable="true" text="概览" />
                <linear dir="h" w="max">
                    <fab color="#57965C" icon="ic_menu_fill" marginRight="15" />
                    <fab color="#C94F4F" icon="ic_person_outline_fill" marginRight="15" />
                    <fab icon="ic_adjust_fill" marginRight="15" size="30" />
                    <fab icon="ic_build_fill" marginRight="15" size="40" />
                    <fab color="#3574F0" icon="ic_settings_fill" />
                </linear>
                <!--基础用法-->
                <text gravity="center" h="50" selectable="true" text="基础用法 监听点击事件" />
                <fab id="mFab" />
                <!--设置主题颜色-->
                <text gravity="center" h="50" selectable="true" text="设置主题颜色 color=颜色" />
                <linear dir="h" w="max">
                    <fab color="#57965C" marginRight="15" />
                    <fab color="#C94F4F" marginRight="15" />
                    <fab color="#3574F0" marginRight="15" />
                    <fab color="#3574F0" />
                </linear>
                <!--设置图标-->
                <text gravity="center" h="50" selectable="true" text="设置图标 icon=图标" />
                <fab icon="ic_image_outline" />
                <!--设置本地图标-->
                <text gravity="center" h="50" selectable="true" text="设置本地图标 path=路径" />
                <fab path="example/$ui - 交互界面/07.fab-悬浮按钮/img/fab-icon.png" />
                <!--设置图标颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置图标颜色 iconTint或者iconColor" />
                <linear dir="h" w="max">
                    <fab iconTint="#57965C" marginRight="15" />
                    <fab iconTint="#C94F4F" marginRight="15" />
                    <fab iconTint="#3574F0" marginRight="15" />
                    <fab />
                </linear>
                <!--设置长按提示(安卓8.0以上支持)-->
                <text gravity="center" h="50" selectable="true"
                    text="设置长按提示(安卓8.0以上支持) tip=提示" />
                <fab icon="ic_build_fill" tip="构建" />
                <!--设置圆弧角度-->
                <text gravity="center" h="50" selectable="true" text="设置圆弧角度 radius=弧度" />
                <linear dir="h" w="max">
                    <fab marginRight="15" radius="10" />
                    <fab marginRight="15" radius="15" />
                    <fab marginRight="15" radius="20" />
                    <fab radius="25" />
                </linear>
                <!--设置尺寸-->
                <text gravity="center" h="50" selectable="true" text="设置尺寸 size=尺寸" />
                <linear dir="h" w="max">
                    <fab marginRight="15" size="30" />
                    <fab marginRight="15" size="35" />
                    <fab marginRight="15" size="40" />
                    <fab size="45" />
                </linear>
                <!--自动显示隐藏-->
                <text gravity="center|start" marginTop="20" selectable="true"
                    text="自动显示隐藏\n在锚点布局(coord)中可以配置一个悬浮按钮自动显示和隐藏\n1.必须在coord布局中\n2.必须要设置behavior=fab:意思是开启悬浮按钮的自动显示和隐藏\n\n我们可以把锚点布局(coord)理解成一个升级版的帧布局(frame):通过layoutGravity属性可以控制悬浮按钮的位置" />
            </linear>
        </nested>
        <!--
        在锚点布局(coord)中可以配置一个悬浮按钮自动显示和隐藏
        1.必须在coord布局中
        2.必须要设置behavior="fab":开启悬浮按钮的自动显示和隐藏
        我们可以把锚点布局(coord)理解成一个升级版的帧布局(frame):通过layoutGravity属性可以控制悬浮按钮的位置
        -->
        <fab behavior="fab" icon="ic_build_fill" layoutGravity="end|bottom" margin="25"
            tip="构建" />
    </coord>
</ui>
`;
// 直接解析布局字符串，无需另建布局文件。
var ui = $ui.layout(layout);
// 按布局中的真实标识查找应用条，返回按钮用于关闭当前界面。
ui.id("mAppbar").back(function () {
    ui.finish();
});
// 点击悬浮按钮时显示提示。
ui.id("mFab").click(function () {
    toast("我被点击了");
});
// 事件设置完毕后显示界面。
ui.show();
```


继续操作英文完整示例中已经创建的界面。
先运行英文示例，再运行这段代码，ui 是前面创建的界面对象。不要重新加载其他控件的布局文件。


```html
// 使用原界面的应用条显示提示，学习控件查找方式。
var appbar = ui.id("mAppbar");
// 本页完整示例已绑定返回事件；点击返回按钮即可结束界面。
log(String(appbar));
```


