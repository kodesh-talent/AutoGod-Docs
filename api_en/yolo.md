# $yolo - 目标检测

- 更新时间:2026-10-22 10:55:52

> 目标检测管理对象（脚本里写作 $yolo），用来创建和管理“AI 认东西”的检测器。
> 
> 它本身不直接检测画面，而是负责：创建检测器（YoloObject）、根据编号找回已创建的检测器、
> 判断某个检测器是否还在、关闭并释放指定的检测器、一键关闭全部。
> 真正的“加载模型、在屏幕/图片上找东西”由创建出来的 YoloObject 去做。
> 
> 典型使用流程：先用 create(版本号) 创建一个检测器对象 → 在这个对象上 init() 加载模型 →
> 用 detect() 在屏幕或图片上找目标 → 用完用 close(编号) 释放。
> 模型文件、模型版本和设备运行库必须匹配；检测速度与精度取决于模型和设备性能。



```javascript
// 首选创建一个检测器对象（版本号按你的模型来，比如 12）
var model = $yolo.create(12);
// 之后就可以在 model 上加载模型、做检测了
```




### create(version)

> 创建一个新的目标检测对象（YoloObject）。
> 
> 首选创建一个对象，传进模型版本号即可。创建出来的对象会被内部记下来，并分到一个唯一编号（id），
> 之后你可以用这个编号通过 get() 把它再找回来。
> 
> 拿到对象后还不算完，必须再调用它的 init() 加载模型文件，才能开始 detect 检测。
> 如果传入的版本号是 null，会直接返回 null。

- 参数 : version {int} 模型版本号（整数，例如 12）；传 null 会返回 null
- 返回 : {YoloObject} 新创建的目标检测对象；版本号为 null 时返回 null
- 版本 : 1.8.3


```javascript
//首选创建一个对象
var yolo12 = $yolo.create(12);
//接下来就可以设置一些基础配置了
yolo12.init("res/yolo.bin", "res/yolo.param", "res/label.txt"); //加载模型
yolo12.setSize(640, 640);     //设置输入尺寸
yolo12.setProbThreshold(0.5); //设置相似度门槛
```


### has(id)

> 判断某个编号对应的检测器是否还活着（还在管理表里）。
> 
> 每个检测器创建后都有一个唯一编号（用 yolo.getId() 拿到）。这个方法用编号去查：
> 返回 true 表示这个检测器还在、还能 get 到；返回 false 表示它已经被 close 关掉了或从来没存在过。

- 参数 : id {string} 检测器的唯一编号（用 yolo.getId() 获得）
- 返回 : {boolean} 该编号对应的检测器还存在返回 true，否则返回 false
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
log($yolo.has(yolo.getId()));//true，刚创建完肯定在
```


### get(id)

> 根据编号把之前创建好的检测器对象重新取出来。
> 
> 典型场景是跨脚本共享同一个检测器：初始化脚本 create 出检测器后，把它的 id 存到 $storage；
> 另一个脚本再用这个 id 通过 get() 把同一个检测器取出来继续用，不用重新创建和加载模型。
> 如果编号找不到对应的检测器，会返回 null。

- 参数 : id {string} 之前 create 出来的检测器编号（用 yolo.getId() 获得）
- 返回 : {YoloObject} 编号对应的检测器对象；找不到则返回 null
- 版本 : 1.8.3


```javascript
//[初始化脚本.js]:
var storage = $storage.create("我的YOLO");
var yolo = $yolo.create(12);
yolo.init("res/yolo.bin", "res/yolo.param", "res/label.txt");
storage.put("mYoloId", yolo.getId()); //把编号存起来给别的脚本用
//[其他脚本.js]:
var storage = $storage.create("我的YOLO");
var yolo = $yolo.get(storage.getStr("mYoloId","null")); //按编号取回检测器
if (yolo != null) {
    var res = yolo.detect(); //直接用它检测
}
```


### close(id)

> 关闭并释放指定编号的检测器，把它占用的内存/显存回收掉。
> 
> 用完一个检测器后应该调用它，否则模型一直占着内存。它会先 recycle 释放底层模型资源，
> 再把这个检测器从管理表里删掉。如果编号不存在则什么也不做。

- 参数 : id {string} 要关闭的检测器编号（用 yolo.getId() 获得）
- 版本 : 1.8.3


```javascript
var yolo = $yolo.create(12);
//拿到id
var id = yolo.getId();
//...用 yolo 做检测...
$yolo.close(id); //用完按编号关闭并释放
```


### closeAll()

> 一次性关闭所有还开着的检测器，全部释放资源。
> 
> 如果你 create 了好几个检测器却没逐个 close，脚本结束前调用它最干净：
> 它会遍历管理表里的每个检测器，逐个 recycle 释放，最后清空整张表。

- 版本 : 1.8.3


```javascript
// 创建了多个检测器后，统一一次性全部关掉
$yolo.closeAll();
```


