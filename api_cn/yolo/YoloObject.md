# YoloObject - 目标检测对象

- 更新时间:2026-10-22 10:55:52

> 目标检测对象（用 $yolo.create(版本号) 得到，例如 $yolo.create(12)）。
> 
> 它能在一张图片或屏幕画面里自动找出“你认识的东西”在哪里，例如找出画面里有几个人、
> 几个按钮、几个图标。用之前要先用 init() 加载训练好的模型文件，再调用 detect() 去检测。
> 
> 新手使用顺序：
> <ol>
>   <li>用 $yolo.create(12) 创建检测对象；</li>
>   <li>用 init() 加载模型（三个文件：bin、param、标签）；</li>
>   <li>用 detect() 截屏检测，或 detect(图片) 检测指定图片；</li>
>   <li>从返回的 YoloResult 里读出找到的每个目标；</li>
>   <li>用完调用 recycle()/close() 释放。</li>
> </ol>



```javascript
//1.创建检测对象（版本号按你模型支持的来）
var yolo = $yolo.create(12);
//2.加载模型文件
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
//3.截一张当前屏幕来检测
var res = yolo.detect();
//4.判断有没有检测成功，并取出找到的目标列表
if (res.isSuccess()) {
    var list = res.getData();          //所有找到的目标
    for (var i = 0; i < list.size(); i++) {
        var cell = list.get(i);        //第 i 个目标
        log("找到目标，中心坐标：" + cell.cx + "," + cell.cy);
    }
}
yolo.recycle();   //5.用完释放
```




### 初始化(模型文件路径, 参数文件路径, 标签文件路径)

> 加载并初始化检测模型（标签放在一个文本文件里，中文方法名“初始化”）。
> 
> 和 init() 是同一个功能，只是方法名用中文。

- 参数 : 模型文件路径 {String} 模型主体文件路径（.bin）
- 参数 : 参数文件路径 {String} 模型参数文件路径（.param）
- 参数 : 标签文件路径 {String} 标签文件路径（.txt）
- 返回 : {YoloResult} 初始化结果
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
var r = yolo.初始化("res/yolo.bin", "res/yolo.param", "res/label.txt");
if (r.isSuccess()) {
    log("模型加载成功");
}
```


### 初始化(模型文件路径, 参数文件路径, 标签)

> 加载并初始化检测模型（标签直接用一串文字，中文方法名“初始化”）。
> 
> 和 init() 一样，区别只是类别名不放在文件里，而是直接用一个字符串数组传进来。

- 参数 : 模型文件路径 {String} 模型主体文件路径（.bin）
- 参数 : 参数文件路径 {String} 模型参数文件路径（.param）
- 参数 : 标签 {List} 类别名字的列表
- 返回 : {YoloResult} 初始化结果
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
//标签直接写成数组：这里举例两个类别
var labels = java.util.Arrays.asList("person", "cellphone");
var r = yolo.初始化("res/yolo.bin", "res/yolo.param", labels);
if (r.isSuccess()) {
    log("模型加载成功");
}
```


### 检测()

> 自动截当前屏幕并检测目标（中文方法名“检测”）。
> 
> 和 detect() 是同一个功能，只是方法名用中文。需要截屏权限。

- 返回 : {YoloResult} 检测结果
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
var res = yolo.检测();       //截当前屏幕并检测
if (res.isSuccess()) {
    log("屏幕上找到了 " + res.getData().size() + " 个目标");
}
```


### 检测(img)

> 在一张指定的图片对象上检测目标（中文方法名“检测”）。
> 
> 和 detect(img) 是同一个功能，只是方法名用中文。

- 参数 : img {Image} 要检测的图片对象
- 返回 : {YoloResult} 检测结果
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
var img = $img.read("res/t01.png");
var res = yolo.检测(img);
if (res.isSuccess()) {
    log("找到了 " + res.getData().size() + " 个目标");
}
```


### 检测(位图)

> 在一个底层位图对象上检测目标（中文方法名“检测”）。
> 
> 和 detect(bitmap) 是同一个功能，只是方法名用中文。

- 参数 : 位图 {Bitmap} 要检测的位图对象
- 返回 : {YoloResult} 检测结果
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
var img = $img.read("res/t01.png");
var res = yolo.检测(img.getBitmap());
log("检测结果：" + res);
```


### 检测(图片路径)

> 直接传入图片文件路径检测目标（中文方法名“检测”）。
> 
> 和 detect(路径) 是同一个功能，只是方法名用中文。

- 参数 : 图片路径 {String} 图片文件路径
- 返回 : {YoloResult} 检测结果
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
var res = yolo.检测("res/test.jpg");
if (res.isSuccess()) {
    log("找到了 " + res.getData().size() + " 个目标");
}
```


### 是初始化的()

> 检查模型是否已经初始化成功（中文方法名“是初始化的”）。
> 
> 和 isInit() 是同一个功能，只是方法名用中文。

- 返回 : {boolean} true 表示已初始化，false 表示未初始化
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
if (yolo.是初始化的()) {
    log("模型已经初始化好了");
} else {
    log("还没初始化");
}
```


### 设置排序方向(方向)

> 设置检测结果的排序方向（中文方法名“设置排序方向”）。
> 
> 排序方向有十几种，默认不排序。传 -1 表示不排序，以免影响速度。

- 参数 : 方向 {int} 排序方向编号；传 -1 表示不排序
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
yolo.设置排序方向(-1);   //不排序，提高速度
```


### 设置尺寸(宽, 高)

> 设置模型输入图片的尺寸（中文方法名“设置尺寸”）。
> 
> 和 setSize(w,h) 是同一个功能，只是方法名用中文。

- 参数 : 宽 {int} 输入宽度
- 参数 : 高 {int} 输入高度
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.设置尺寸(640, 640);
```


### 设置使用gpu(使用)

> 设置是否使用 GPU 加速检测（中文方法名“设置使用gpu”）。
> 
> 和 setUseGpu() 是同一个功能，只是方法名用中文。

- 参数 : 使用 {boolean} true 用 GPU，false 用 CPU
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.设置使用gpu(true);   //开启 GPU 加速
```


### 设置相似度(相似度)

> 设置概率阈值（中文方法名“设置相似度”）。
> 
> 把握程度大于这个门槛的目标才会被保留。门槛越高越准但越少，越低越多但可能误报。

- 参数 : 相似度 {float} 阈值，0 到 1 之间的小数
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.设置相似度(0.5);   //只保留把握超过 50% 的目标
```


### 设置抑制阈值(抑制阈值)

> 设置“非极大值抑制阈值”（中文方法名“设置抑制阈值”）。
> 
> 用来去掉同一个目标上重复重叠的框。新手一般保持默认即可。

- 参数 : 抑制阈值 {float} 0 到 1 之间的小数
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.设置抑制阈值(0.5);
```


### 设置均值(均值)

> 设置图片预处理时用到的“均值”（中文方法名“设置均值”）。
> 
> 按模型给的说明填写三个颜色通道的值，新手一般用默认即可。

- 参数 : 均值 {float[]} 三个颜色通道的均值数组
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.设置均值([0.485, 0.456, 0.406]);
```


### 设置归一化(归一化)

> 设置图片预处理时用到的“归一化参数”（中文方法名“设置归一化”）。
> 
> 按模型说明填写，新手一般用默认即可。

- 参数 : 归一化 {float[]} 三个颜色通道的归一化系数
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.设置归一化([0.00392, 0.00392, 0.00392]);
```


### 设置输入层(输入层名称)

> 设置模型“输入层”的名字（中文方法名“设置输入层”）。
> 
> 输入层一般只有一个，名字按模型文档填写。

- 参数 : 输入层名称 {String} 输入层的名字
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.设置输入层("data");
```


### 设置输出层(输出层名称1)

> 设置模型“输出层”的名字（只有一个输出层时，中文方法名“设置输出层”）。
> 
> 有些模型只有一个输出层，用这个方法填它的名字即可。

- 参数 : 输出层名称1 {String} 输出层的名字
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.设置输出层("detection_out");
```


### 设置输出层(输出层名称1, 输出层名称2, 输出层名称3)

> 设置模型“输出层”的名字（有多个输出层时，中文方法名“设置输出层”）。
> 
> 有些模型有多个输出层，可以一次填三个；如果实际只有一个，也只会生效第一个。

- 参数 : 输出层名称1 {String} 第 1 个输出层名字
- 参数 : 输出层名称2 {String} 第 2 个输出层名字
- 参数 : 输出层名称3 {String} 第 3 个输出层名字
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.设置输出层("layer1", "layer2", "layer3");
```


### 获取id()

> 获取这个检测对象的唯一编号（中文方法名“获取id”）。
> 
> 和 getId() 是同一个功能，只是方法名用中文。

- 返回 : {String} 这个对象的唯一编号
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
log("这个检测对象的 id 是：" + yolo.获取id());
```


### 释放资源()

> 释放这个检测对象占用的资源（中文方法名“释放资源”）。
> 
> 释放资源，和 close() 效果等价。用完模型后记得调用。

- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
//...做检测...
yolo.释放资源();
```


### 关闭()

> 关闭这个检测对象，释放资源（中文方法名“关闭”）。
> 
> 释放资源，和 recycle() 效果等价。

- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
//...做检测...
yolo.关闭();
```


