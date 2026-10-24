# 综合案例

- 更新时间:2026-10-22 10:58:42



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
            <appbar back="true" id="mAppbar" scrollFlags="scroll|enterAlways" subTitle="轨道"
                title="Rail" w="max" />
        </appbar-layout>
        <!--滑动布局 在锚点布局中可以配置控件行为是:适配应用条-->
        <nested behavior="appbar" h="max" w="max">
            <!--线性布局:被滑动布局包裹，子控件较多时允许向下滑动-->
            <!--padding:增加内边距[左,上,右,下]-->
            <linear h="max" padding="20,20,20,100" w="max">
                <frame w="max">
                    <!--配置菜单-->
                    <rail>
                        <menu icon="ic_home_fill" text="主页" />
                        <menu icon="ic_menu_fill" text="菜单" />
                        <menu icon="ic_settings_fill" text="设置" />
                    </rail>
                    <!--设置图标颜色 iconTint-->
                    <rail iconTint="#C94F4F" marginStart="80">
                        <menu icon="ic_home_fill" text="主页" />
                        <menu icon="ic_menu_fill" text="菜单" />
                        <menu icon="ic_settings_fill" text="设置" />
                    </rail>
                    <!--设置文本颜色 textColor-->
                    <rail marginStart="160" textColor="#C94F4F">
                        <menu icon="ic_home_fill" text="主页" />
                        <menu icon="ic_menu_fill" text="菜单" />
                        <menu icon="ic_settings_fill" text="设置" />
                    </rail>
                    <!--设置选中颜色 checkColor-->
                    <rail checkColor="#C94F4F" marginStart="240">
                        <menu icon="ic_home_fill" text="主页" />
                        <menu icon="ic_menu_fill" text="菜单" />
                        <menu icon="ic_settings_fill" text="设置" />
                    </rail>
                </frame>
                <frame w="max">
                    <!--设置背景颜色 bg-->
                    <rail bg="#C94F4F">
                        <menu icon="ic_home_fill" text="主页" />
                        <menu icon="ic_menu_fill" text="菜单" />
                        <menu icon="ic_settings_fill" text="设置" />
                    </rail>
                    <!--设置背景图片 bgImg-->
                    <rail bgImg="example/$ui - 交互界面/18.rail-轨道/img/img.png" marginStart="80">
                        <menu icon="ic_home_fill" text="主页" />
                        <menu icon="ic_menu_fill" text="菜单" />
                        <menu icon="ic_settings_fill" text="设置" />
                    </rail>
                </frame>
            </linear>
        </nested>
    </coord>
</ui>
`;
var ui = $ui.layout(layout);
```


## JS代码


```javascript
var ui = $ui.layout("example/$ui - 交互界面/10.input-输入框/input.xml");
//绑定标题栏返回按钮
ui.id("mAppbar").back(function(){
    ui.finish();
});
//先获取控件
var mButton = ui.id("mButton");
var mInput = ui.id("mInput");
//找到按钮、点击按钮的时候就显示输入框的内容
mButton.click(function(){
    //获取输入框的内容
    var content = mInput.getText();
    //显示输入框的内容
    mButton.snack("内容:"+content);
});
//显示界面
ui.show();
```


