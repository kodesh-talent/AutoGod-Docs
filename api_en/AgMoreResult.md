# 多个结果

- 更新时间:2026-10-22 10:55:45

> 多候选查找的结果对象，保存命中位置和候选下标。
> 
> point 的类型为 Point，包含整数 x、y；index 的类型为 int，下标从零开始。
> 候选可能是图片、颜色组合或区域，index 的具体含义取决于调用哪个 $ag 方法。
> 默认构造得到 point 为 null、index 为 -1 的空结果。部分查找接口没命中会返回 null，部分返回这样的空结果，因此应同时检查对象、下标和点。
> findImgsOne 的 data 每项应为参数对象，不能只填路径字符串；若无效图片或范围被跳过，下标对应过滤后的有效候选顺序。
> 下例只练习读取结果，不需要截图权限或图片文件，也不代表真的检测到目标。



```javascript
var result = new AgMoreResult(); // 创建教学结果，不会查找图片。
result.point = new Point(100, 200); // 放入一个点对象。
result.index = 0; // 零表示第一项，不是第一百项或坐标。
if (result != null && result.index >= 0 && result.point != null) {
    log(result.index + ":" + result.point.getX() + "," + result.point.getY()); // 继续读取点对象。
}
```




### const {Point} point;

> 保存命中位置的点对象。
> 
> 类型为 Point，默认值为 null，表示尚未保存位置。Point 的 x、y 为整数坐标。
> 这是公开字段，可以直接读取或赋值；保存的是对象引用，不会复制点。修改点的 x、y 会改变这份结果中的位置。
> 实际坐标含义以返回它的查找方法为准；赋值只修改数据，不会点击屏幕，也不会改变 index。


```javascript
var result = new AgMoreResult(); // 创建教学结果，不会查找图片。
result.point = new Point(100, 200); // 放入一个点对象。
result.index = 0; // 零表示第一项，不是第一百项或坐标。
var point = result.point; // 取出嵌套的点对象。
if (point != null) {
    log(point.getX() + "," + point.getY()); // 安全读取两个整数坐标。
    point.setX(120); // 修改共享的点对象。
    log(result.point.x); // 结果中的横坐标也变成一百二十。
}
```


### const {int} index;

> 保存命中候选的下标。
> 
> 类型为 int（整数），默认 -1 表示尚未命中；零对应第一项，一对应第二项。
> 具体是图片下标、颜色组下标还是区域下标，由产生结果的接口决定。
> findImgsOne 会跳过加载失败的图片或无效范围，返回下标可能属于过滤后的有效候选序列，不一定是原 data 数组的下标。
> 这个公开字段不会检查赋值是否合法；手动改成零也不会自动生成 point，读取位置前仍需判空。


```javascript
var result = new AgMoreResult(); // 创建教学结果，不会查找图片。
result.point = new Point(100, 200); // 放入一个点对象。
result.index = 0; // 零表示第一项，不是第一百项或坐标。
if (result.index >= 0 && result.point != null) {
    log("候选序号：" + (result.index + 1)); // 给人看的序号通常从一开始。
    log(result.point.x + "," + result.point.y); // 同时确认保存的位置。
}
```


### getPoint()

> 读取保存的命中位置。
> 
> 没有输入参数；返回类型为 Point，未保存位置时返回 null。
> 返回原来的点对象引用，不是副本，等价于读取 point 字段；不会执行新的查找。
> 可以继续调用点对象的 getX、getY；调用前先判断是不是 null。

- 返回 : {Point} 当前保存的点对象，可能为 null


```javascript
var result = new AgMoreResult(); // 创建教学结果，不会查找图片。
result.point = new Point(100, 200); // 放入一个点对象。
result.index = 0; // 零表示第一项，不是第一百项或坐标。
var point = result.getPoint(); // 得到 Point 对象或 null。
if (point != null) {
    log(point.getX()); // 读取整数横坐标。
    log(point.getY()); // 读取整数纵坐标。
}
```


### getIndex()

> 读取保存的候选下标。
> 
> 没有输入参数；返回类型为 int（整数），初始值为 -1。零表示第一项。
> 方法只读取 index，不检查 point，也不验证候选是否仍存在。实际使用时应同时检查位置。
> 当查找接口过滤掉无效候选时，不要直接用返回值索引原始候选数组，需先确认两者顺序一致。

- 返回 : {int} 当前保存的候选下标，默认 -1


```javascript
var result = new AgMoreResult(); // 创建教学结果，不会查找图片。
result.point = new Point(100, 200); // 放入一个点对象。
result.index = 0; // 零表示第一项，不是第一百项或坐标。
var index = result.getIndex(); // 读取整数下标。
var point = result.getPoint(); // 读取嵌套的点对象。
if (index >= 0 && point != null) {
    log(index + ":" + point.getX() + "," + point.getY()); // 展示完整结果。
}
```


