# gravity-重力属性对照表

- 更新时间:2026-10-22 10:58:38



#### 使用方法


```html
// 将布局文字保存在字符串中；每一行用加号连接，符合 ES5 语法。
// 中英文示例任选一套运行。图片资源需提前放到布局所写的路径。
var layout =
    "<ui>\n" +
    "    <statusbar/>\n" +
    "    <!-- 这里的 gravity 重力值，可以决定子组件(按钮)在布局中的位置 center 表示让按钮居中 -->\n" +
    "    <linear w=\"max\" h=\"max\" gravity=\"center\">\n" +
    "        <button text=\"按钮\"/>\n" +
    "    </linear>\n" +
    "</ui>\n";
// 解析字符串得到界面对象，不需要另建布局文件。
var ui = $ui.layout(layout);
// 绑定好事件后再显示界面。
ui.show();
```


#### Gravity属性值对照表

| 属性值                                        | 对应的Gravity值                     |
|--------------------------------------------|---------------------------------|
| fill、填充                                    | Gravity.FILL                    |
| fill_h、fill_horizontal、水平填充、横向填充           | Gravity.FILL_HORIZONTAL         |
| fill_v、fill_vertical、垂直填充、竖向填充             | Gravity.FILL_VERTICAL           |
| start、开头、开始、头部                             | Gravity.START                   |
| end、末尾、结束、尾部                               | Gravity.END                     |
| left、左、左边                                  | Gravity.LEFT                    |
| right、右、右边                                 | Gravity.RIGHT                   |
| top、上、上边                                   | Gravity.TOP                     |
| bottom、下、下边、下面                             | Gravity.BOTTOM                  |
| center、中、中心、中间、居中                          | Gravity.CENTER                  |
| center_h、center_horizontal、水平居中、横向居中       | Gravity.CENTER_HORIZONTAL       |
| center_v、center_vertical、垂直居中、竖向居中         | Gravity.CENTER_VERTICAL         |
| display_h、display_horizontal、水平显示裁剪、横向显示裁剪 | Gravity.DISPLAY_CLIP_HORIZONTAL |
| display_v、display_vertical、垂直显示裁剪、竖向显示裁剪   | Gravity.DISPLAY_CLIP_VERTICAL   |
| clip_h、clip_horizontal、水平裁剪、横向裁剪           | Gravity.CLIP_HORIZONTAL         |
| clip_v、clip_vertical、垂直裁剪、竖向裁剪             | Gravity.CLIP_VERTICAL           |

:::tip 注意
由于脚本支持中文和英文编程，所以重力属性值可以采用中文，也可以采用英文。

例如：gravity="center"

等同：重力="中"
:::


