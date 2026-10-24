# 综合案例

- 更新时间:2026-10-22 10:58:40



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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="图片与图标"
                title="Img" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <!--概览-->
                <text gravity="center" h="50" selectable="true" text="概览" />
                <linear dir="h" w="max">
                    <img h="220" marginEnd="15"
                        path="example/$ui - 交互界面/09.img-图片图标/img/img_0.png" w="100" />
                    <img h="220" marginEnd="15"
                        path="example/$ui - 交互界面/09.img-图片图标/img/img_1.png" w="100" />
                    <img h="220" path="example/$ui - 交互界面/09.img-图片图标/img/img_2.png"
                        w="100" />
                </linear>
                <!--基础用法-->
                <text gravity="center" h="50" selectable="true" text="基础用法 设置图片" />
                <linear dir="v" gravity="center" w="max">
                    <!--简单的示例:点击按钮的时候会设置头像-->
                    <button id="setImg" text="设置头像" />
                    <!--放置一个圆形图片-->
                    <img h="100" id="headImg" w="100" />
                </linear>
                <!--设置弧度-->
                <text gravity="center" h="50" selectable="true" text="设置弧度 radius=弧度" />
                <linear dir="h" gravity="center" w="max">
                    <img h="60" marginEnd="15"
                        path="example/$ui - 交互界面/09.img-图片图标/img/img_3.png" radius="10"
                        w="60" />
                    <img h="60" marginEnd="15"
                        path="example/$ui - 交互界面/09.img-图片图标/img/img_3.png" radius="20"
                        w="60" />
                    <img h="60" path="example/$ui - 交互界面/09.img-图片图标/img/img_3.png"
                        radius="30" w="60" />
                </linear>
                <!--设置链接-->
                <text gravity="center" h="50" selectable="true" text="设置链接 url=qq头像链接" />
                <img h="60" radius="30" url="https://q1.qlogo.cn/g?b=qq&nk=2540645055&s=100"
                    w="60" />
                <!-- 设置边框宽度 -->
                <text gravity="center" h="50" selectable="true"
                    text="设置边框宽度 strokeWidth=宽度" />
                <linear dir="h" gravity="center" w="max">
                    <!-- 原图 -->
                    <img h="60" path="example/$ui - 交互界面/09.img-图片图标/img/img.png" w="60" />
                    <!-- 设置边框的图 -->
                    <img h="60" marginEnd="15" marginStart="15"
                        path="example/$ui - 交互界面/09.img-图片图标/img/img.png" strokeWidth="10"
                        w="60" />
                </linear>
                <!--设置边框颜色-->
                <text gravity="center" h="50" selectable="true"
                    text="设置边框颜色 strokeColor=颜色" />
                <linear dir="h" gravity="center" w="max">
                    <!--原图-->
                    <img h="60" path="example/$ui - 交互界面/09.img-图片图标/img/img.png" w="60" />
                    <!--设置边框的图-->
                    <img h="60" marginEnd="15" marginStart="15"
                        path="example/$ui - 交互界面/09.img-图片图标/img/img.png" strokeWidth="10"
                        w="60" />
                    <!--设置边框颜色的图-->
                    <img h="60" path="example/$ui - 交互界面/09.img-图片图标/img/img.png"
                        strokeColor="#553574F0" strokeWidth="10" w="60" />
                </linear>
                <!--设置填充颜色-->
                <text gravity="center" h="50" selectable="true" text="设置填充颜色 tint=颜色" />
                <linear dir="h" gravity="center" w="max">
                    <!--原图-->
                    <img h="60" marginEnd="15"
                        path="example/$ui - 交互界面/09.img-图片图标/img/boy.png" w="60" />
                    <!--设置填充颜色的图-->
                    <img h="60" marginEnd="15"
                        path="example/$ui - 交互界面/09.img-图片图标/img/boy.png" tint="#57965C"
                        w="60" />
                    <img h="60" path="example/$ui - 交互界面/09.img-图片图标/img/boy.png"
                        tint="#C94F4F" w="60" />
                </linear>
                <!--设置图片路径-->
                <text gravity="center" h="50" selectable="true" text="设置图片路径 path=路径" />
                <linear dir="h" gravity="center" w="max">
                    <img h="100" marginEnd="15"
                        path="example/$ui - 交互界面/09.img-图片图标/img/img_5.png" w="60" />
                </linear>
                <!--设置图标-->
                <text gravity="center" h="50" selectable="true" text="设置图标 src/icon=图标" />
                <linear dir="h" gravity="center" w="max">
                    <!--使用src来设置图标-->
                    <img h="30" src="ic_near_me_fill" w="30" />
                    <!--使用icon来设置图标-->
                    <img h="30" icon="ic_adb_fill" marginStart="15" w="30" />
                </linear>
                <!--设置旋转角度-->
                <text gravity="center" h="50" selectable="true"
                    text="设置旋转角度 rotation=旋转角度" />
                <linear dir="h" gravity="center" w="max">
                    <img h="60" path="example/$ui - 交互界面/09.img-图片图标/img/img_4.png"
                        rotation="10" w="60" />
                    <img h="60" marginEnd="15" marginStart="15"
                        path="example/$ui - 交互界面/09.img-图片图标/img/img_4.png" rotation="30"
                        w="60" />
                    <img h="60" path="example/$ui - 交互界面/09.img-图片图标/img/img_4.png"
                        rotation="60" w="60" />
                </linear>
                <!--设置自动旋转-->
                <text gravity="center" h="50" selectable="true"
                    text="设置自动旋转 rotate=是否自动旋转 rotateSpeed=旋转速度" />
                <linear dir="h" gravity="center" w="max">
                    <img h="60" rotate="true" src="ic_audiotrack_outline" w="60" />
                    <img h="60" marginEnd="15" marginStart="15" rotate="true" rotateSpeed="10"
                        src="ic_audiotrack_outline" w="60" />
                    <img h="60" rotate="true" rotateSpeed="20" src="ic_audiotrack_outline" w="60" />
                </linear>
                <!--设置内边距-->
                <text gravity="center" h="50" selectable="true" text="设置内边距 padding=内边距" />
                <linear dir="h" gravity="center" w="max">
                    <img h="60" path="example/$ui - 交互界面/09.img-图片图标/img/img_6.png"
                        w="60" />
                    <img h="60" marginEnd="15" marginStart="15" padding="5"
                        path="example/$ui - 交互界面/09.img-图片图标/img/img_6.png" w="60" />
                    <img h="60" padding="10"
                        path="example/$ui - 交互界面/09.img-图片图标/img/img_6.png" w="60" />
                </linear>
                <!--设置背景颜色-->
                <text gravity="center" h="50" selectable="true" text="设置背景颜色 bg=背景颜色" />
                <img bg="#5557965C" h="60"
                    path="example/$ui - 交互界面/09.img-图片图标/img/img_7.png" w="max" />
                <img bg="#55C94F4F" h="60"
                    path="example/$ui - 交互界面/09.img-图片图标/img/img_7.png" w="max" />
                <!--设置背景图片-->
                <text gravity="center" h="50" selectable="true"
                    text="设置背景图片 bgImg=背景图片" />
                <img bgImg="example/$ui - 交互界面/09.img-图片图标/img/img_8.png" h="min"
                    path="example/$ui - 交互界面/09.img-图片图标/img/img_9.png" radius="30"
                    w="max" />
            </linear>
        </nested>
    </coord>
</ui>
`;
var ui = $ui.layout(layout);
```


## JS代码


```javascript
var ui = $ui.layout("example/$ui - 交互界面/02.button-按钮/button.xml");
//绑定标题栏返回按钮
ui.id("appbar").back(function(){
    ui.finish();
});
//找到按钮并且设置点击事件
ui.id("button").click(function(){
    toast("我被点击了");
});
//显示界面
ui.show();
```


