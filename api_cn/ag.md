# $ag - 图色框架

- 更新时间:2026-10-22 10:55:45

> 图色识别框架对象（脚本里写作 $ag），是“找图找色”自动化的核心。
> 
> 它会自动截屏，然后在屏幕画面里找你给的小图模板、找指定颜色，找到了就返回坐标（Point），
> 还能顺带帮你点击那个位置。常用能力分几块：
> <ul>
>     <li>找图：findImg / waitImg / findImgClick，传模板图片路径；</li>
>     <li>找色：findColor / waitColor / findColorClick，传十六进制颜色；</li>
>     <li>多点找色：findMultiColors，靠一组相关颜色点定位，更抗皮肤变化；</li>
>     <li>多目标：findImgsOne / findColorsOne / findImgInRegions，一次给多个候选，命中哪个返回哪个；</li>
>     <li>血条：bloodPercent，根据血条颜色算出还剩百分之多少。</li>
> </ul>
> 识别结果通常是一个 Point（点坐标），Point 自带 x、y 两个数字；多目标结果是 AgMoreResult，里面有 point 和 index（命中第几个）。
> 截图和模板文件需能被应用读取（建议把模板图放到 /sdcard 下）。



```javascript
//最简单的找图：在全屏找一张按钮图，找到就得到它的中心坐标
var point = $ag.findImg({
    path: "/sdcard/target.png",        //模板图片路径
    region: [0, 0, 1080, 1920],        //只在这个矩形范围[x,y,宽,高]里找
    similar: 0.8,                       //相似度，0~1，越高越严格
    trans: false                        //模板是否带透明背景
});
if (point != null) {
    log("找到了，坐标：" + point.x + "," + point.y);
}
```




### setDebug(debug)

> 开启或关闭调试模式。
> 
> 默认是开启调试模式的(推荐开启:更加直观的看到执行效果),找到图片则会在屏幕上绘制图片的位置,找到颜色则绘制点。
> 调试时会在屏幕上画出找到的图框/色点，方便你肉眼确认找得准不准；上线前可以关掉。

- 参数 : debug {boolean} true 开启调试绘制，false 关闭
<p>教学示例：
<pre>{@code
$ag.setDebug(true);
var result = $ag.findImg({path: "/sdcard/target.png"});
log("调试结果：" + result);
}</pre>


```javascript
$ag.setDebug(true); //打开调试，找图找色时会在屏幕上画出位置
```


### findImg(options)

> 找图（只截屏找一次，找到就返回，找不到返回 null）。
> 
> 自动截一张当前屏幕，在指定范围里和你给的模板小图做比对，相似度够了就算找到。
> 返回的 Point 是模板图片“中心点”在屏幕上的坐标（不是左上角）。

- 参数 : options {object} 找图参数对象，见上方示例的 path/region/similar/trans
- 返回 : {Point} 找到返回图片中心点坐标 Point（含 x、y）；没找到返回 null
- 版本 : 1.0.0


```javascript
//参数:
var options = {
    path: "/sdcard/target.png",     //模板图片路径（必填）
    region: [0, 0, 1080, 1920],    //只在[x,y,宽,高]这个范围找；不传则全屏
    similar: 0.8,                    //相似度0~1，默认0.8，越高越严格
    trans: false                     //模板是否带透明背景（透明处不参与匹配）
};
//使用:
var point = $ag.findImg(options);
if (point != null) {
    log("找到图片，中心坐标：" + point.x + "," + point.y);
}
```


### findImgClick(options)

> 找图并点击（找到图片后自动点它的中心点）。
> 
> 先截屏一次,如果图片找到了,那么就点击这个图片位置中心点。
> 点哪里可以用 px/py 在中心点基础上再偏移；还能设点击次数、点击间隔。

- 参数 : options {obj} 找图+点击参数对象，字段同 findImg，另加 px/py/clickTime/clickDur/clickDelay
- 返回 : {Point} 找到并点击后返回图片中心点坐标；没找到返回 null
- 版本 : 1.0.0


```javascript
//参数:
var options = {
    path: "/sdcard/btn.png",         //模板图片路径
    region: [0, 0, 1080, 1920],      //查找范围[x,y,宽,高]
    similar: 0.8,                      //相似度
    trans: false,                     //是否透明背景
    px: 0, //(可选)点击位置相对于中点的x偏移量
    py: 0, //(可选)点击位置相对于中点的y偏移量
    clickTime: 1,                     //(可选)找到后点几下，默认1
    clickDur: 800                     //(可选)每点一下后停多久(毫秒)
};
//使用:找到按钮图就点它
var point = $ag.findImgClick(options);
if (point != null) {
    log("已点击按钮：" + point.x + "," + point.y);
}
```


### waitImg(options, failCallback)

> 等待图片出现（循环截屏找图，直到找到或达到最大次数）。
> 
> 截屏后找图没找到就会执行回调一次,然后就继续截屏并且找图。
> 
> 和 findImg 不同，这个会“反复等”：每隔 waitDur 毫秒截一次屏找一次图，最多找 waitTimes 次。
> 
> 还可以开启“二次确认”（ensure），避免画面闪了一下就误判：
> <ul>
>     <li>ensureMode 设为 "once"：连续找 ensureTimes 次里只要有 1 次找到，就算真找到了；</li>
>     <li>ensureMode 设为 "more"：必须连续 ensureTimes 次都找到，才算真找到了（更稳）。</li>
> </ul>
> 确认执行完毕之后,会返回找到的位置,如果没有找到,则继续等待图片,每次找图都会执行确认流程。
> 
> 整体流程是：
> 1.先截屏一次
> 2.在范围内按相似度找图
> 3.找到了就走确认流程，确认通过就返回该位置
> 4.如果确认流程没有通过(执行回调),那么就继续截屏并且执行回到1

- 参数 : options {object} 等待找图参数对象，字段见上方 path/region/similar/waitTimes/waitDur/ensure 等
- 参数 : failCallback {function(curTimes)} 每一轮没找到时回调一次，curTimes 是已经试过的轮数（从0开始）
- 返回 : {Point} 在次数用完前找到就返回图片中心点坐标；一直没找到返回 null


```javascript
var options = {
    path: "/sdcard/target.png",     //模板图片路径
    region: [0, 0, 1080, 1920],    //查找范围[x,y,宽,高]
    similar: 0.8,                    //相似度0~1
    trans: false,                   //是否透明背景
    waitTimes: 30,                   //最多找多少次（轮）
    waitDur: 800,                    //每轮之间停顿多少毫秒
    ensure: true,                    //是否开启二次确认
    ensureMode: "once",             //确认模式：once=找到一次即算，more=连续多次都要找到
    ensureTimes: 3,                  //每轮里确认找几次
    ensureDur: 300                   //每次确认之间停顿毫秒
};
//使用:一直等这张图出现，等不到就打印已经试了多少轮
var point = $ag.waitImg(options, function(curTimes) {
    log("第 " + curTimes + " 轮还没找到，继续等");
});
if (point != null) {
    log("等到图片了：" + point.x + "," + point.y);
}
```


### waitImg(options)

> 等待图片出现（不关心每轮失败，只等最终结果）。
> 
> 作用和 waitImg(options, 回调) 完全一样，只是每轮没找到时不做额外处理，安静地继续等。

- 参数 : options {object} 等待找图参数对象，字段同上一个 waitImg
- 返回 : {Point} 等到就返回图片中心点坐标，一直等不到返回 null


```javascript
var options = {
    path: "/sdcard/target.png",     //模板图片路径
    region: [0, 0, 1080, 1920],    //查找范围[x,y,宽,高]
    similar: 0.8,                    //相似度0~1
    trans: false,                   //是否透明背景
    waitTimes: 30,                   //最多找多少轮
    waitDur: 800,                    //每轮间隔毫秒
    ensure: true,                    //是否二次确认
    ensureMode: "once",             //确认模式
    ensureTimes: 3,                  //确认几次
    ensureDur: 300                   //确认间隔毫秒
};
var point = $ag.waitImg(options);
if (point != null) {
    log("等到图片：" + point.x + "," + point.y);
}
```


### waitImgClick(options, failCallback)

> 等待图片出现，找到后自动点击。
> 
> 和 waitImg 一样反复等图，区别是一旦等到图片，就自动点它的中心点（可用 px/py 偏移）。

- 参数 : options {obj} 等待找图+点击参数对象，字段同 waitImg，另加 px/py/clickTime 等
- 参数 : failCallback {function(curTimes)} 每轮没找到时回调一次，curTimes 是已试轮数
- 返回 : {point} 等到并点击后返回图片中心点坐标；一直没等到返回 null


```javascript
var options = {
    path: "/sdcard/btn.png",         //模板图片路径
    region: [0, 0, 1080, 1920],      //查找范围[x,y,宽,高]
    similar: 0.8,                      //相似度
    trans: false,                     //是否透明背景
    waitTimes: 30,                     //最多等多少轮
    waitDur: 800,                      //每轮间隔毫秒
    ensure: true,                      //是否二次确认
    ensureMode: "once",               //确认模式
    ensureTimes: 3,                    //确认几次
    ensureDur: 300,                    //确认间隔毫秒
    px: 0, //(可选)点击位置相对于中点的x偏移量
    py: 0, //(可选)点击位置相对于中点的y偏移量
    clickTime: 1                      //(可选)点几下
}
var point = $ag.waitImgClick(options, function(curTimes) {
    log("第 " + curTimes + " 轮还没等到按钮");
});
if (point != null) {
    log("等到并点击了按钮");
}
```


### waitImgClick(options)

> 等待图片出现并点击（不关心每轮失败）。
> 
> 作用和 waitImgClick(options, 回调) 完全一样，只是每轮没找到时不做额外处理。

- 参数 : options {object} 等待找图+点击参数对象，字段同上一个 waitImgClick
- 返回 : {point} 等到并点击后返回图片中心点坐标；一直没等到返回 null


```javascript
var options = {
    path: "/sdcard/btn.png",         //模板图片路径
    region: [0, 0, 1080, 1920],      //查找范围[x,y,宽,高]
    similar: 0.8,                      //相似度
    trans: false,                     //是否透明背景
    waitTimes: 30,                     //最多等多少轮
    waitDur: 800,                      //每轮间隔毫秒
    ensure: true,                      //是否二次确认
    ensureMode: "once",               //确认模式
    ensureTimes: 3,                    //确认几次
    ensureDur: 300,                    //确认间隔毫秒
    px: 0, //(可选)点击位置相对于中点的x偏移量
    py: 0, //(可选)点击位置相对于中点的y偏移量
    clickTime: 1                      //(可选)点几下
}
var point = $ag.waitImgClick(options);
if (point != null) {
    log("等到并点击了按钮");
}
```


### findImgInRegions(options)

> 在多个候选区域里找同一张图（找到哪个区域命中就返回哪个）。
> 
> 给定一个范围数组,只能在指定的范围数组当中查找对应的图片,找到后,返回图片的位置和数组下标。
> 
> 执行流程:先截屏,然后循环每个范围数组,对小图片进行查找，找到之后就立马返回。
> 
> 使用场景:比如关闭广告的[关闭按钮],有时候这个关闭按钮出现在右上角,有时候出现在中间下方的位置,在这种不确定关闭图片位置的情况下，使用此函数，将可能出现关闭按钮的位置全部传入，找到后即可返回位置。

- 参数 : options {object} 参数对象：path 模板图、region 候选区域数组、similar 相似度、trans 透明背景
- 返回 : {AgMoreResult} 命中返回结果对象，含 point（坐标）和 index（命中了 region 里第几个区域）；候选区域有效但都没命中时返回 point 为 null、index 为 -1 的空结果；参数解析为空或区域列表为空时可能返回 null


```javascript
//关闭按钮可能出现在右上角或底部，把两块区域都传进去
var options = {
    path: "/sdcard/close.png",          //关闭按钮模板图
    similar: 0.9,                         //相似度
    trans: false,                        //是否透明背景
    region: [                            //候选区域数组，每个是[x,y,宽,高]
        [800, 0, 280, 200],              //右上角那块
        [300, 1500, 480, 200]            //底部中间那块
    ]
};
var result = $ag.findImgInRegions(options);
if (result != null && result.index >= 0 && result.point != null) {
    log("在第 " + result.index + " 个区域找到了关闭按钮");
    log("坐标：" + result.point.x + "," + result.point.y);
}
```


### findImgsOne(options)

> 一次给多张候选图，找到其中任意一张就立即返回（只截屏找一次）。
> 
> 传入多组图片数据,截屏后找图,只要其中有一组数据成功找到,则直接返回结果。
> 
> 适用的场景：比如我们每次打开游戏或者应用界面的时候，我们并不知道它会不会弹出来一个更新界面或者广告界面,此时我们可以使用此函数,把可能出现的界面情况都传入进去,只要找到了,那么就会返回执行结果,我们就能知道是哪一个界面了。

- 参数 : options {obj} 参数对象：data 为候选图参数数组（每项含 path/region/similar/trans）
- 返回 : {AgMoreResult} 命中返回结果对象（point 坐标 + index 命中第几张），都没命中返回 null


```javascript
//data 是一个数组，每项都是一张候选图的参数
var options = {
    data: [
        {
            path: "/sdcard/update.png",      //候选图1：更新提示
            region: [0, 0, 1080, 1920],       //它的查找范围
            similar: 0.8,                      //它的相似度
            trans: false
        },
        {
            //...多个这样的数据（候选图2：广告界面）
            path: "/sdcard/ad.png",
            region: [0, 0, 1080, 1920],
            similar: 0.8
        }
    ]
};
var result = $ag.findImgsOne(options);
if (result != null) {
    log("命中了第 " + result.index + " 张候选图");
}
```


### waitImgsOne(options)

> 循环等待多张候选图，哪张先出现就返回哪张。
> 
> 传入多组图片数据,截屏后找图,只要其中有一组数据成功找到,则直接返回结果。
> 
> 和 findImgsOne 的区别：findImgsOne 只找一次，这个会每隔 waitDur 毫秒重复找，最多找 waitTimes 轮。
> 
> 适用的场景：比如我们每次打开游戏或者应用界面的时候，我们并不知道它会不会弹出来一个更新界面或者广告界面,此时我们可以使用次函数,把可能出现的界面情况都传入进去,只要找到了,那么就会返回执行结果,我们就能知道是哪一个界面了。

- 参数 : options {obj} 参数对象：data 候选图数组、waitTimes 等待轮数、waitDur 每轮间隔
- 返回 : {AgMoreResult} 先命中的图返回结果对象（point 坐标 + index 命中第几张），等满都没命中返回 null


```javascript
var options = {
    data: [
        {
            path: "/sdcard/update.png",      //候选图1
            region: [0, 0, 1080, 1920],
            similar: 0.8,
            trans: false
        },
        {
            //...多个这样的数据（候选图2）
        }
    ],
    waitTimes: 30,                            //最多等多少轮
    waitDur: 800                              //每轮间隔毫秒
};
var result = $ag.waitImgsOne(options);
if (result != null) {
    log("先出现的是第 " + result.index + " 张图");
}
```


### waitImgsOne(options, failCallback)

> 循环等待多张候选图，可在每轮都没命中时收到回调。
> 
> 作用和 waitImgsOne(options) 一样，只是多一个失败回调：每一轮所有候选图都没命中时回调一次，方便你打印日志或做分析。

- 参数 : options {obj} 参数对象：data 候选图数组、waitTimes 等待轮数、waitDur 每轮间隔
- 参数 : failCallback {function(curTimes)} 每轮都没命中时回调，curTimes 是已试轮数
- 返回 : {AgMoreResult} 先命中的图返回结果对象（point 坐标 + index 命中第几张），等满都没命中返回 null


```javascript
var options = {
    data: [
        {
            path: "/sdcard/update.png",      //候选图1
            region: [0, 0, 1080, 1920],
            similar: 0.8,
            trans: false
        },
        {
            //...多个这样的数据（候选图2）
        }
    ],
    waitTimes: 30,                            //最多等多少轮
    waitDur: 800                              //每轮间隔毫秒
};
var result = $ag.waitImgsOne(options, function(curTimes) {
    log("第 " + curTimes + " 轮都没等到任何候选图");
});
if (result != null) {
    log("先出现的是第 " + result.index + " 张图");
}
```


### clickImgWhileNot(options)

> 循环点击某张图片，直到这张图片消失（或达到最大次数）。
> 
> 使用场景：比如在一些比较卡顿的应用或游戏中,我希望点击关闭按钮,但是游戏界面比较卡顿,可以使用此函数不断的点击,直到关闭成功。
> 逻辑是：每轮找到图就点一下，然后继续找；一旦某轮找不到图了（说明它消失了）就结束。

- 参数 : options {obj} 参数对象，字段同 waitImg（path/region/similar/waitTimes/waitDur/px/py 等）
- 返回 : {point} 图片消失前最后一次找到的坐标；一开始就没找到返回 null


```javascript
var options = {
    path: "/sdcard/close.png",       //要反复点的图
    region: [0, 0, 1080, 1920],      //查找范围[x,y,宽,高]
    similar: 0.8,                      //相似度
    trans: false,                     //是否透明背景
    waitTimes: 10,                     //最多循环多少轮（防止死循环）
    waitDur: 500,                      //每轮之间停多久
    ensure: false,                     //是否二次确认
    ensureMode: "once",
    ensureTimes: 3,
    ensureDur: 300,
    px: 0, //(可选)点击位置相对于中点的x偏移量
    py: 0, //(可选)点击位置相对于中点的y偏移量
    clickTime: 1                     //(可选)每轮点几下
}
var point = $ag.clickImgWhileNot(options);
log("循环点击结束，最后一次找到：" + point);
```


### clickImgWhileNot(options, failCallback)

> 循环点击某张图片直到它消失，图片消失时会触发一次失败回调。
> 
> 使用场景：比如游戏人物打开背包后要存放苹果,此时我们可以使用此函数不断的点击苹果,把它存放到背包中。
> 和无回调版区别：一旦某轮找不到图（图片消失了），结束前会先调一次 failCallback，你可以在里面做收尾处理。

- 参数 : options {obj} 参数对象，字段同 waitImg
- 参数 : failCallback {function(curTimes)} 图片消失（结束）时回调一次，curTimes 是已循环轮数
- 返回 : {point} 图片消失前最后一次找到的坐标；一开始就没找到返回 null


```javascript
var options = {
    path: "/sdcard/apple.png",        //要反复点的苹果图标
    region: [0, 0, 1080, 1920],      //查找范围[x,y,宽,高]
    similar: 0.8,                      //相似度
    trans: false,                     //是否透明背景
    waitTimes: 20,                     //最多循环多少轮
    waitDur: 500,                      //每轮之间停多久
    ensure: false,
    ensureMode: "once",
    ensureTimes: 3,
    ensureDur: 300,
    px: 0, //(可选)点击位置相对于中点的x偏移量
    py: 0, //(可选)点击位置相对于中点的y偏移量
    clickTime: 1
}
var point = $ag.clickImgWhileNot(options, function(curTimes) {
    log("苹果已经点完消失了，已点 " + curTimes + " 轮");
});
```


### bloodPercent(options)

> 血条检测：算出指定区域里“血条颜色”已经填了百分之多少。
> 
> 主要根据传入的颜色(可传入多个颜色以,分割)和血条的范围来计算出血条的百分比。
> 原理是把血条横向切成很多小段，从左到右逐段看有没有血条颜色，连续有颜色的段数占比就是血量百分比。

- 参数 : options {object} 参数对象：region 血条范围、color 血条颜色、threshold 颜色容差
- 返回 : {int} 血量百分比 0~100；检测失败（完全没颜色）返回 -1


```javascript
//血条大致在屏幕左上角这块，血条是红色
var options = {
    region: [50, 200, 400, 30],       //血条所在矩形[x,y,宽,高]
    color: "#FF3030",                  //血条颜色（可多个用逗号分隔）
    threshold: 5                       //颜色容差
};
var p = $ag.bloodPercent(options);     //返回 0~100 的整数百分比
log("当前血量：" + p + "%");
```


### findColor(options)

> 找色（在指定范围内找第一个出现目标颜色的点）。
> 
> 自动截屏，在 region 范围内寻找颜色值接近 color 的像素点。color 可传多个，用逗号分隔，找到任一即可。
> 返回第一个匹配到的点的坐标 Point。

- 参数 : options {object} 参数对象：region 查找范围、color 目标颜色、threshold 颜色容差
- 返回 : {Point} 找到返回匹配点坐标（含 x、y）；范围内没找到返回 null


```javascript
var options = {
    region: [0, 0, 300, 300],        //只在这块区域[x,y,宽,高]里找
    color: "#ff0000",                  //要找的颜色（十六进制）
    threshold: 5                       //颜色容差，越大越宽松
};
var point = $ag.findColor(options);
if (point != null) {
    log("找到红点：" + point.x + "," + point.y);
}
```


### findMultiColors(options)

> 多点找色：先找到一个“主色”，再看它周围几个“辅助色点”的相对位置对不对得上。
> 
> 多点找色比单点找色更准：它要求主色和若干个辅助色点的相对偏移都和你写的一致，才认定找到了，不容易误判。
> 多点找色并不能很好的适配全分辨率,因为把颜色点相对位置写死了,而不同的设备中,相对点位不同。

- 参数 : options {object} 参数对象：color 主色、region 范围、threshold 主色容差、multiColors 辅助色点数组
- 返回 : {point} 全部点都对上返回主色点坐标 Point；对不上返回 null


```javascript
var options = {
    color: "#ff0000",                   //主色（先找到这个点当基准）
    region: [0, 0, 1080, 1920],        //查找范围[x,y,宽,高]
    threshold: 5,                        //主色容差
    multiColors: [                       //辅助色点数组，每个点是[相对x,相对y,"颜色",容差]
        [10, 5, "#00ff00", 5],           //在主色右边10、下方5处应有一个绿色点
        [20, 8, "#0000ff", 5]           //...多个点色
    ]
};
var point = $ag.findMultiColors(options);
if (point != null) {
    log("多点找色命中，主色点：" + point.x + "," + point.y);
}
```


### findMultiColorsClick(options)

> 多点找色并点击：多点找色命中后，自动点那个主色点。

- 参数 : options {object} 参数对象，字段同 findMultiColors，另加 px/py 点击偏移
- 返回 : {point} 命中并点击后返回主色点坐标；没命中返回 null


```javascript
var options = {
    color: "#ff0000",                   //主色
    region: [0, 0, 1080, 1920],        //查找范围[x,y,宽,高]
    threshold: 5,                        //主色容差
    multiColors: [                       //辅助色点数组
        [10, 5, "#00ff00", 5],
        //...多个点色
    ],
    px:0, //(可选)点击位置x偏移量
    py:0 //(可选)点击位置y偏移量
}
var point = $ag.findMultiColorsClick(options);
if (point != null) {
    log("多点找色命中并已点击");
}
```


### waitMultiColors(options)

> 等待多点找色命中（循环截屏直到命中或达到次数）。

- 参数 : options {object} 参数对象，字段同 findMultiColors，另支持 waitTimes/waitDur/ensure 等等待参数
- 返回 : {point} 等到命中返回主色点坐标；等满次数没命中返回 null


```javascript
var result = $ag.waitMultiColors({ color: "#ff0000", region: [0, 0, 300, 300] });
if (result != null) {
    log("等到多点色：" + result.x + "," + result.y);
}
```


### waitMultiColorsClick(options)

> 等待多点找色命中，命中后自动点击主色点。

- 参数 : options {object} 参数对象，字段同 findMultiColors，另加等待参数和 px/py 点击偏移
- 返回 : {point} 命中并点击后返回主色点坐标；没命中返回 null


```javascript
var result = $ag.waitMultiColorsClick({ color: "#ff0000", region: [0, 0, 300, 300] });
if (result != null) {
    log("等到多点色并已点击");
}
```


### waitMultiColors(options, failCallback)

> 等待多点找色命中，可在每轮未命中时收到回调。
> 
> 循环截屏做多点找色，直到命中或达到最大轮数；每轮没命中都会调一次 failCallback。

- 参数 : options {object} 参数对象，字段见上方 color/region/multiColors/waitTimes/ensure 等
- 参数 : failCallback {function(curTimes)} 每轮未命中时回调，curTimes 是已试轮数
- 返回 : {point} 命中返回主色点坐标；等满轮数没命中返回 null


```javascript
var options = {
    color: "#ff0000",                   //主色
    region: [0, 0, 1080, 1920],        //查找范围[x,y,宽,高]
    threshold: 5,                        //主色容差
    multiColors: [                       //辅助色点数组[相对x,相对y,"颜色",容差]
        [10, 5, "#00ff00", 5],
        [20, 8, "#0000ff", 5]
    ],
    waitTimes: 30,                       //最多等多少轮
    waitDur: 800,                        //每轮间隔毫秒
    ensure: true,                        //是否二次确认
    ensureMode: "once",                 //确认模式
    ensureTimes: 3,                      //确认几次
    ensureDur: 300                       //确认间隔毫秒
}
var point = $ag.waitMultiColors(options, function(curTimes) {
    log("第 " + curTimes + " 轮多点色还没对上");
});
```


### waitMultiColorsClick(options, failCallback)

> 等待多点找色命中并点击，每轮未命中可收到回调。
> 
> 循环等待多点找色，一旦命中就自动点主色点；每轮没命中调一次 failCallback。

- 参数 : options {obj} 参数对象，字段同 findMultiColors，另加等待参数和 px/py
- 参数 : failCallback {function(curTimes)} 每轮未命中时回调，curTimes 是已试轮数
- 返回 : {point} 命中并点击后返回主色点坐标；没命中返回 null


```javascript
var result = $ag.waitMultiColorsClick({ color: "#ff0000", region: [0, 0, 300, 300] }, function(curTimes) {
    log("第 " + curTimes + " 轮还没等到多点色");
});
```


### findColorClick(options)

> 找色并点击：找到颜色点后自动点它。

- 参数 : options {object} 参数对象：region 查找范围、color 目标颜色、threshold 容差，另加 px/py 点击偏移
- 返回 : {point} 找到并点击后返回该点坐标；没找到返回 null


```javascript
var result = $ag.findColorClick({ color: "#ff0000", region: [0, 0, 300, 300] });
if (result != null) {
    log("找到红点并已点击：" + result.x + "," + result.y);
}
```


### waitColor(options, failCallback)

> 等待某颜色出现（循环找色，直到找到或达到最大轮数）。
> 
> 每隔 waitDur 毫秒截一次屏找一次色，最多找 waitTimes 轮。也可开启二次确认（ensure）防止画面闪烁误判。

- 参数 : options {obj} 等待找色参数对象，字段见上方 region/color/threshold/waitTimes/ensure 等
- 参数 : failCallback {function(curTimes)} 每轮没找到时回调，curTimes 是已试轮数
- 返回 : {point} 等到就返回颜色点坐标；等满轮数没等到返回 null


```javascript
var options = {
    region: [0, 0, 1080, 1920],        //查找范围[x,y,宽,高]
    color: "#ff0000",                   //要等的颜色
    threshold: 5,                        //颜色容差
    waitTimes: 30,                       //最多找多少轮
    waitDur: 800,                        //每轮间隔毫秒
    ensure: true,                        //是否二次确认
    ensureMode: "once",                 //确认模式：once=找到一次即算，more=连续多次都要找到
    ensureTimes: 3,                      //确认几次
    ensureDur: 300                       //确认间隔毫秒
}
var point = $ag.waitColor(options, function(curTimes) {
    log("第 " + curTimes + " 轮还没等到该颜色");
});
if (point != null) {
    log("等到颜色：" + point.x + "," + point.y);
}
```


### waitColor(options)

> 等待某颜色出现（不关心每轮失败）。
> 
> 作用和 waitColor(options, 回调) 一样，只是每轮没找到时不做额外处理。

- 参数 : options {obj} 等待找色参数对象，字段同上一个 waitColor
- 返回 : {point} 等到就返回颜色点坐标；等满轮数没等到返回 null


```javascript
var options = {
    region: [0, 0, 1080, 1920],        //查找范围[x,y,宽,高]
    color: "#ff0000",                   //要等的颜色
    threshold: 5,                        //颜色容差
    waitTimes: 30,                       //最多找多少轮
    waitDur: 800,                        //每轮间隔毫秒
    ensure: true,                        //是否二次确认
    ensureMode: "once",
    ensureTimes: 3,
    ensureDur: 300
}
var point = $ag.waitColor(options);
if (point != null) {
    log("等到颜色：" + point.x + "," + point.y);
}
```


### waitColorWhileNot(options, failCallback)

> 等待某颜色消失（颜色还在就反复找，一旦找不到了就结束）。
> 
> 常用来等一个加载条、菊花、弹窗颜色消失，表示界面加载完了。每轮还能找到颜色时会回调一次，找不到了就返回。

- 参数 : options {obj} 参数对象，字段同 waitColor
- 参数 : failCallback {function(curTimes)} 每轮还能找到颜色时回调一次，curTimes 是已试轮数


```javascript
var options = {
    region: [0, 0, 1080, 1920],        //要监控的范围[x,y,宽,高]
    color: "#ff0000",                   //要等它消失的颜色
    threshold: 5,                        //颜色容差
    waitTimes: 30,                       //最多等多少轮
    waitDur: 800,                        //每轮间隔毫秒
    ensure: false,                       //是否二次确认
    ensureMode: "once",
    ensureTimes: 3,
    ensureDur: 300
}
$ag.waitColorWhileNot(options, function(curTimes) {
    log("第 " + curTimes + " 轮该颜色还在，继续等");
});
log("颜色已经消失了");
```


### waitColorClick(options, failCallback)

> 等待某颜色出现，出现后自动点击该点。

- 参数 : options {obj} 参数对象，字段同 waitColor，另加 px/py 点击偏移
- 参数 : failCallback {function(curTimes)} 每轮没找到时回调，curTimes 是已试轮数
- 返回 : {point} 等到并点击后返回颜色点坐标；没等到返回 null


```javascript
var result = $ag.waitColorClick({ color: "#ff0000", region: [0, 0, 300, 300] }, function(curTimes) {
    log("第 " + curTimes + " 轮还没等到该颜色");
});
if (result != null) {
    log("等到颜色并已点击");
}
```


### waitColorClick(options)

> 等待某颜色出现并点击（不关心每轮失败）。

- 参数 : options {obj} 参数对象，字段同 waitColor，另加 px/py 点击偏移
- 返回 : {point} 等到并点击后返回颜色点坐标；没等到返回 null


```javascript
var result = $ag.waitColorClick({ color: "#ff0000", region: [0, 0, 300, 300] });
if (result != null) {
    log("等到颜色并已点击");
}
```


### findColorInRegions(options)

> 在多个候选区域里找同一个颜色（命中哪个区域就返回哪个）。
> 
> 和 findImgInRegions 思路一样，只是把“找图”换成“找色”。color 可传多个用逗号分隔。

- 参数 : options {object} 参数对象：color 目标颜色、threshold 容差、region 候选区域数组
- 返回 : {AgMoreResult} 命中返回结果对象（point 坐标 + index 命中第几个区域），候选区域有效但都没命中时返回 point 为 null、index 为 -1 的空结果；参数解析为空或区域列表为空时可能返回 null


```javascript
//红色按钮可能在屏幕上半或下半，把两块区域都传进去
var options = {
    color: "#ff0000",                  //要找的颜色
    threshold: 5,                       //颜色容差
    region: [                           //候选区域数组，每个是[x,y,宽,高]
        [0, 0, 1080, 500],             //上半屏
        [0, 1200, 1080, 720]           //下半屏
    ]
};
var result = $ag.findColorInRegions(options);
if (result != null && result.index >= 0 && result.point != null) {
    log("在第 " + result.index + " 个区域找到颜色");
    log(result.point.getX() + "," + result.point.getY()); // 读取命中像素的坐标。
}
```


### findColorsOne(options)

> 一次给多组“区域+颜色”，找到其中任意一组就立即返回。
> 
> 传入多组找色条件（每组各自有自己的查找范围和颜色），截一张屏依次比对，哪组先命中就返回哪组。
> 适合判断“当前屏幕上出现了哪种提示色”。

- 参数 : options {object} 参数对象：data 为找色条件数组（每项含 region/color/threshold）
- 返回 : {AgMoreResult} 命中返回结果对象（point 坐标 + index 命中第几组），都没命中返回 null


```javascript
var options = {
    data: [
        { region: [0, 0, 500, 500], color: "#ff0000", threshold: 5 },  //第1组：左上是否有红色
        { region: [500, 0, 500, 500], color: "#00ff00", threshold: 5 } //第2组：右上是否有绿色
    ]
};
var result = $ag.findColorsOne(options);
if (result != null) {
    log("命中了第 " + result.index + " 组颜色");
    log("坐标：" + result.point.x + "," + result.point.y);
}
```


### closeDraw()

> 关闭绘制的图案
> 


```javascript
$ag.closeDraw();
```

```javascript
$ag.closeDraw();
log("已关闭识图调试绘制");
```


