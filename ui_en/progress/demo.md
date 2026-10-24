# 综合案例

- 更新时间:2026-10-22 10:58:41



## Xml代码


```javascript
// 将布局内容作为字符串传入解析方法；返回值是可查找控件的界面对象。
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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="进度条"
                title="Progress" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--概览-->
                <text gravity="center" h="50" selectable="true" text="概览" />
                <linear dir="h" w="max">
                    <progress padding="10" run="true" w="max" />
                    <progress color="#518855" padding="10" run="true" w="max" />
                    <progress color="#B44A4A" padding="10" run="true" w="max" />
                </linear>
                <progress style="line" padding="10" run="true" w="max" />
                <progress style="line" color="#518855" padding="10" run="true" w="max" />
                <progress style="line" color="#B44A4A" padding="10" run="true" w="max" />
                <!--基础使用-->
                <text gravity="center" h="50" selectable="true" text="基础使用" />
                <progress style="line" id="progress" padding="10" w="max" />
                <button id="download" text="开始下载" w="max" />
                <!--设置显示-->
                <text gravity="center" h="50" selectable="true"
                    text="设置显示 visible=false 第一个显示了，第二个被隐藏了" />
                <linear dir="h" w="max">
                    <progress padding="10" visible="true" w="max" />
                    <progress padding="10" visible="false" w="max" />
                </linear>
                <!--设置风格-->
                <text gravity="center" h="50" selectable="true" text="设置风格 style=风格" />
                <!--没设置风格-->
                <progress padding="10" w="max" />
                <!--设置直线风格-->
                <progress style="line" padding="10" w="max" />
                <!--设置厚度(dp)-->
                <text gravity="center" h="50" selectable="true" text="设置厚度 thickness=厚度" />
                <progress padding="10" thickness="10" w="max" />
                <progress style="line" padding="10" thickness="10" w="max" />
                <!--设置播放动画-->
                <text gravity="center" h="50" selectable="true" text="设置播放动画 run=true" />
                <progress padding="10" run="true" w="max" />
                <progress style="line" padding="10" run="true" w="max" />
                <!--设置主题颜色-->
                <text gravity="center" h="50" selectable="true" text="设置主题颜色 color=颜色" />
                <progress color="#57965C" padding="10" run="true" w="max" />
                <progress style="line" color="#C94F4F" padding="10" run="true" w="max" />
                <!--设置内边距(dp)-->
                <text gravity="center" h="50" selectable="true" text="设置内边距 padding=内边距" />
                <linear dir="h" w="max">
                    <progress padding="10" />
                    <progress padding="20" />
                    <progress padding="30" />
                </linear>
                <!--设置背景颜色-->
                <text gravity="center" h="50" selectable="true" text="设置背景颜色 bg=颜色" />
                <progress bg="#57965C" padding="10" run="true" w="max" />
                <progress style="line" bg="#C94F4F" padding="10" run="true" w="max" />
                <!--设置背景图片-->
                <text gravity="center" h="50" selectable="true"
                    text="设置背景图片 bgImg=背景图片" />
                <progress bgImg="example/$ui - 交互界面/16.progress-进度条/img/img_1.png"
                    padding="10" run="true" w="max" />
                <progress style="line" bgImg="example/$ui - 交互界面/16.progress-进度条/img/img.png"
                    padding="10" run="true" w="max" />
            </linear>
        </nested>
    </coord>
</ui>
`;
var ui = $ui.layout(layout);
```


