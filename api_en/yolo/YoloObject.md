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




### init(binPath, paramPath, labelPath)

> 加载并初始化检测模型（标签放在一个文本文件里）。
> 
> 检测之前必须先调用它把模型文件读进来。需要三个文件：
> <ul>
>   <li>binPath：模型主体文件（.bin）；</li>
>   <li>paramPath：模型参数文件（.param）；</li>
>   <li>labelPath：标签文件（.txt，每行一个类别名）。</li>
> </ul>
> 返回一个 YoloResult，用它的 isSuccess() 判断是否加载成功。

- 参数 : binPath {String} 模型主体文件路径（.bin）
- 参数 : paramPath {String} 模型参数文件路径（.param）
- 参数 : labelPath {String} 标签文件路径（.txt）
- 返回 : {YoloResult} 初始化结果，用 isSuccess() 看是否成功
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
//加载模型，三个文件都放在 res 目录
var r = yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
if (r.isSuccess()) {
    log("模型加载成功，可以开始检测了");
} else {
    log("模型加载失败：" + r.getDes());
}
```


### init(binPath, paramPath, labels)

> 加载并初始化检测模型（标签直接用一个字符串数组传进来）。
> 
> 和 init(三个文件) 一样，只是类别名不放在 label.txt 文件里，
> 而是直接用一个 List（字符串数组）传进来。

- 参数 : binPath {String} 模型主体文件路径（.bin）
- 参数 : paramPath {String} 模型参数文件路径（.param）
- 参数 : labels {List} 类别名字的列表
- 返回 : {YoloResult} 初始化结果
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
var labels = java.util.Arrays.asList("person", "cellphone");
var r = yolo.init("res/yolo.bin", "res/yolo.param", labels);
if (r.isSuccess()) {
    log("模型加载成功");
}
```


### detect()

> 自动截一张当前屏幕，然后在屏幕上检测目标。
> 
> 它会先截屏，再用加载好的模型去找东西。注意：这个功能需要已开启截屏权限。
> 返回 YoloResult，从中读出找到的所有目标。

- 返回 : {YoloResult} 检测结果，用 getData() 取目标列表
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
var res = yolo.detect();     //截当前屏幕并检测
if (res.isSuccess()) {
    var list = res.getData();
    log("屏幕上找到了 " + list.size() + " 个目标");
}
```


### detect(img)

> 在一张指定的图片对象上检测目标。
> 
> 参数 img 是一个 Image 图片对象（用 $img.read 读出来的，或截屏得到的）。
> 如果你传进去的图片是空的，会返回一个 success 为 false 的结果。

- 参数 : img {Image} 要检测的图片对象（$img.read 得到）
- 返回 : {YoloResult} 检测结果
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
var img = $img.read("res/t01.png");     //先读一张图片
var res = yolo.detect(img);             //在这张图上检测
if (res.isSuccess()) {
    var list = res.getData();
    for (var i = 0; i < list.size(); i++) {
        log("第" + i + "个目标中心：" + list.get(i).cx);
    }
}
```


### detect(bitmap)

> 在一个底层位图对象上检测目标。
> 
> 参数 bitmap 是 Android 的位图对象，一般由 Image 对象的 getBitmap() 得到。
> 新手更常用 detect(图片对象) 这种写法。

- 参数 : bitmap {Bitmap} 要检测的位图对象（由图片.getBitmap() 得到）
- 返回 : {YoloResult} 检测结果
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
var img = $img.read("res/t01.png");
var res = yolo.detect(img.getBitmap());  //传入底层位图
log("检测结果：" + res);
```


### detect(imgPath)

> 直接传入图片文件路径，检测该图片里的目标。
> 
> 它会自己按路径把图片读进来再检测，省去你先 $img.read 的步骤。

- 参数 : imgPath {String} 图片文件路径
- 返回 : {YoloResult} 检测结果
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
var res = yolo.detect("res/test.jpg");   //直接传图片路径
if (res.isSuccess()) {
    log("找到了 " + res.getData().size() + " 个目标");
}
```


### isInit()

> 检查模型是否已经初始化成功。
> 
> 返回 true 表示模型已加载好，可以直接 detect；false 表示还没 init 成功。

- 返回 : {boolean} true 表示已初始化，false 表示未初始化
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
if (yolo.isInit()) {
    log("模型已经初始化好了");
} else {
    log("还没初始化，需要先调用 init");
}
```


### setDir(dir)

> 设置检测结果的排序方向。
> 
> 检测到多个目标后，可以让它们按某种顺序排好（例如从上到下、从左到右）。
> 一共有十几种排序方向，传 -1 表示不排序（不排序会更快）。

- 参数 : dir {int} 排序方向编号；传 -1 表示不排序
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
yolo.setDir(-1);   //不需要排序，提高速度
```


### setSize(w, h)

> 设置模型输入图片的尺寸（宽和高）。
> 
> 模型只会按固定大小去“看”图片。一般用模型要求的默认尺寸即可，
> 例如 640 乘 640。

- 参数 : w {int} 输入宽度（像素）
- 参数 : h {int} 输入高度（像素）
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.setSize(640, 640);   //输入尺寸设为 640x640
```


### setUseGpu(use)

> 设置是否使用 GPU 加速检测。
> 
> 传 true 表示用显卡（GPU）跑，通常更快；传 false 用 CPU 跑。
> 不是所有设备/模型都支持 GPU，按实际情况开启。

- 参数 : use {boolean} true 用 GPU，false 用 CPU
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.setUseGpu(true);   //开启 GPU 加速
```


### setProbThreshold(pt)

> 设置“概率阈值”（也叫置信度门槛）。
> 
> 模型每次框出一个目标都会给一个把握程度（0 到 1 之间的小数）。
> 只有把握程度大于这个门槛的目标才会被保留。门槛越高，结果越少但越准；
> 门槛越低，结果越多但可能误报。

- 参数 : pt {float} 概率阈值，0 到 1 之间的小数
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.setProbThreshold(0.5);   //只保留把握超过 50% 的目标
```


### setNmsThreshold(nt)

> 设置“非极大值抑制阈值”。
> 
> 同一个东西可能被模型框出好几个重叠的框，这个阈值用来决定重叠到什么程度
> 就算“同一个东西”，只保留把握最高的那个。新手一般保持默认即可。

- 参数 : nt {float} 抑制阈值，0 到 1 之间的小数
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.setNmsThreshold(0.5);
```


### setMeanVals(meanVals)

> 设置图片预处理时用到的“均值”。
> 
> 这是模型训练时约定的数值，一般按模型给的说明填，三个数分别对应三个颜色通道。
> 新手用模型默认即可，不一定要改。

- 参数 : meanVals {float[]} 三个颜色通道的均值数组
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.setMeanVals([0.485, 0.456, 0.406]);   //按模型说明填写
```


### setNormVals(normVals)

> 设置图片预处理时用到的“归一化参数”。
> 
> 把像素颜色从 0~255 缩放到模型需要的范围时用到的系数，按模型说明填。
> 新手用默认即可。

- 参数 : normVals {float[]} 三个颜色通道的归一化系数
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.setNormVals([0.00392, 0.00392, 0.00392]);   //1/255
```


### setInputName(inputName)

> 设置模型“输入层”的名字。
> 
> 一个模型由很多层组成，数据从“输入层”进去。一般模型只有一个输入层，
> 名字按模型文档给的填写即可。

- 参数 : inputName {String} 输入层的名字
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.setInputName("data");   //按模型文档填输入层名字
```


### setOutputName(outputName1)

> 设置模型“输出层”的名字（只有一个输出层时用这个）。
> 
> 检测结果从输出层出来。如果你的模型只有一个输出层，就用这个方法填它的名字。

- 参数 : outputName1 {String} 输出层的名字
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.setOutputName("detection_out");   //按模型文档填输出层名字
```


### setOutputName(outputName1, outputName2, outputName3)

> 设置模型“输出层”的名字（有多个输出层时用这个，最多三个）。
> 
> 有些版本的模型有多个输出层，最多可以一次填三个。
> 如果你的模型其实只有一个输出层，填三个也只会生效第一个。

- 参数 : outputName1 {String} 第 1 个输出层名字
- 参数 : outputName2 {String} 第 2 个输出层名字
- 参数 : outputName3 {String} 第 3 个输出层名字
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.setOutputName("layer1", "layer2", "layer3");   //按模型文档填
```


### getId()

> 获取这个检测对象的唯一编号（ID）。
> 
> 每个用 $yolo.create 创建出来的对象都有一个独一无二的编号，一般用于区分多个检测对象。

- 返回 : {String} 这个对象的唯一编号
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
log("这个检测对象的 id 是：" + yolo.getId());
```


### recycle()

> 释放这个检测对象占用的资源。
> 
> 用完模型后应该调用它，把内存和显存释放掉。它和 close() 效果一样。

- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
//...做检测...
yolo.recycle();   //用完释放
```


### close()

> 关闭这个检测对象，释放资源。
> 
> 和 recycle() 效果完全一样，只是另一个名字。用完模型后调用它释放内存。

- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
//...做检测...
yolo.close();   //用完关闭
```


