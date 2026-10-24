# YoloResult - 检测结果

- 更新时间:2026-10-22 10:56:19

> 一次目标检测的整体结果，包含状态、文字说明和目标列表。
> 
> 实际检测通常由 $yolo 创建的检测器提供；本类只保存结果，直接 new 不会加载模型或分析图片。
> 先判断 isSuccess()，再查看 getData()。成功和找到目标不是同一件事：成功结果也可能是空列表。
> getData() 返回 Java 列表，使用 size() 和 get(下标)；其中每项是 YoloResultCell，可继续读取标签、分数和坐标。
> 下面用教学数据演示完整结构，手动设置成功只改变状态，不代表真的运行过检测。



```javascript
var result = new YoloResult(); // 构造教学结果，不会执行检测。
var cell = new YoloResultCell(); // 创建一条目标数据。
cell.setLabel("phone"); cell.setSimilar(0.92); // 填写类别和分数。
var list = new java.util.ArrayList(); // 创建 Java 列表，不是脚本数组。
list.add(cell); // 把目标对象放入列表。
result.setData(list); // 复制列表容器，目标对象仍由双方共享。
result.setSuccess(true); // 仅标记这份教学数据的状态。
var cells = result.getData(); // 读取当前列表。
for (var i = 0; i < cells.size(); i++) { // 空列表时不进入循环。
    var item = cells.get(i); // 下标从零开始。
    if (item != null) { // 手动构造的列表可能放入空项。
        log(item.getLabel() + ":" + item.getSimilar()); // 继续读取目标对象的成员。
    }
}
```




### const {boolean} 成功;

> 保存是否成功。
> 
> 类型为 boolean，初始值为 false。这是私有字段，脚本需要通过公开方法访问。
> 使用 isSuccess() 读取，setSuccess(值) 设置。设置方法同时更新英文和中文字段，但不会自动修改其他状态或文字。
> true 只表示保存的成功标志；不能据此保证目标列表至少有一项。
> 当前没有对应的中文公开方法；示例使用中文变量名，方法名保留本类实际提供的英文名称。


```javascript
var 结果 = new YoloResult(); // 创建教学结果。
日志(结果.isSuccess()); // 查看初始值。
结果.setSuccess(true); // 只改这一类数据。
日志(结果.isSuccess()); // 检查新值。
```


### const {String} 描述;

> 保存结果说明。
> 
> 类型为 String，初始值为 “处理失败”。这是私有字段，脚本需要通过公开方法访问。
> 使用 getDes() 读取，setDes(值) 设置。设置方法同时更新英文和中文字段，但不会自动修改其他状态或文字。
> 文字可以被设置成 null；不要仅凭提示文字判断成功与否，应读取 isSuccess()。
> 当前没有对应的中文公开方法；示例使用中文变量名，方法名保留本类实际提供的英文名称。


```javascript
var 结果 = new YoloResult(); // 创建教学结果。
日志(结果.getDes()); // 查看初始值。
结果.setDes("教学数据已准备"); // 只改这一类数据。
日志(结果.getDes()); // 检查新值。
```


### const {String} 异常;

> 保存错误说明。
> 
> 类型为 String，初始值为 “暂无异常”。这是私有字段，脚本需要通过公开方法访问。
> 使用 getErr() 读取，setErr(值) 设置。设置方法同时更新英文和中文字段，但不会自动修改其他状态或文字。
> 文字可以被设置成 null；不要仅凭提示文字判断成功与否，应读取 isSuccess()。
> 当前没有对应的中文公开方法；示例使用中文变量名，方法名保留本类实际提供的英文名称。


```javascript
var 结果 = new YoloResult(); // 创建教学结果。
日志(结果.getErr()); // 查看初始值。
结果.setErr("教学错误说明"); // 只改这一类数据。
日志(结果.getErr()); // 检查新值。
```


### const {List<YoloResultCell>} 数据;

> 保存目标对象列表。
> 
> 类型为 List<YoloResultCell>（Java 列表，每项是单个目标对象），初始为空列表。
> 这是私有字段，脚本应使用 getData() 和 setData(...)，不能直接访问这个字段。
> data 与 数据 是不同列表，不保证始终同步；getData() 返回英文列表。setData 会分别复制输入列表，但里面的目标对象仍共享。
> 当前检测装配过程会向中文列表重复追加英文列表内容，因此不要把两份存储当成相同列表。
> 本类没有中文取列表方法，中文脚本仍需调用实际存在的 getData 和 setData。


```javascript
var 结果 = new YoloResult(); // 构造教学结果，不会执行检测。
var 目标 = new YoloResultCell(); // 创建一条目标数据。
目标.setLabel("手机"); 目标.setSimilar(0.92); // 填写类别和分数。
var 列表 = new java.util.ArrayList(); // 创建 Java 列表，不是脚本数组。
列表.add(目标); // 把目标对象放入列表。
结果.setData(列表); // 复制列表容器，目标对象仍由双方共享。
var 目标列表 = 结果.getData(); // 读取当前列表。
for (var 序号 = 0; 序号 < 目标列表.size(); 序号++) { // 空列表时不进入循环。
    var 条目 = 目标列表.get(序号); // 下标从零开始。
    if (条目 != null) { // 手动构造的列表可能放入空项。
        日志(条目.getLabel() + ":" + 条目.getSimilar()); // 继续读取目标对象的成员。
    }
}
```


### setSuccess(success)

> 设置是否成功。
> 
> 初始值为 false。成功状态不代表列表中一定有目标。
> 设置方法同时更新对应的中英文存储，但不会自动改变其他字段，也不会触发模型检测。
> 输入类型为 boolean；返回 void，无返回值。

- 参数 : success {boolean} 要保存的是否成功
- 返回 : {void} 无返回值


```javascript
var result = new YoloResult(); // 构造教学结果。
log(result.isSuccess()); // 查看初始值。
result.setSuccess(true); // 设置这一项数据。
log(result.isSuccess()); // 查看设置后的值。
```


### getDes()

> 读取结果说明。
> 
> 初始值为 “处理失败”。文字允许为 null。
> 设置方法同时更新对应的中英文存储，但不会自动改变其他字段，也不会触发模型检测。
> 没有输入参数，返回 String 类型的当前英文存储值。

- 返回 : {String} 当前保存的结果说明


```javascript
var result = new YoloResult(); // 构造教学结果。
log(result.getDes()); // 查看初始值。
result.setDes("sample ready"); // 设置这一项数据。
log(result.getDes()); // 查看设置后的值。
```


### setDes(des)

> 设置结果说明。
> 
> 初始值为 “处理失败”。文字允许为 null。
> 设置方法同时更新对应的中英文存储，但不会自动改变其他字段，也不会触发模型检测。
> 输入类型为 String；返回 void，无返回值。

- 参数 : des {String} 要保存的结果说明
- 返回 : {void} 无返回值


```javascript
var result = new YoloResult(); // 构造教学结果。
log(result.getDes()); // 查看初始值。
result.setDes("sample ready"); // 设置这一项数据。
log(result.getDes()); // 查看设置后的值。
```


### getData()

> 读取目标列表。
> 
> 列表类型为 List<YoloResultCell>，每项是包含类别、分数和坐标的目标对象。
> setData 会复制两份列表容器，但不复制每个目标对象；之后修改输入列表的长度不影响保存列表，修改共享目标对象的字段则会影响读取结果。
> getData 返回内部英文列表本身，不是副本；对它增删会直接改变结果，不会同步中文列表。
> 没有输入参数，返回初始为空的列表。不要未检查长度就 get(0)，列表中的空项也应先判断。

- 返回 : {List<YoloResultCell>} 当前内部英文目标列表


```javascript
var result = new YoloResult(); // 构造教学结果，不会执行检测。
var cell = new YoloResultCell(); // 创建一条目标数据。
cell.setLabel("phone"); cell.setSimilar(0.92); // 填写类别和分数。
var list = new java.util.ArrayList(); // 创建 Java 列表，不是脚本数组。
list.add(cell); // 把目标对象放入列表。
result.setData(list); // 复制列表容器，目标对象仍由双方共享。
var cells = result.getData(); // 读取当前列表。
for (var i = 0; i < cells.size(); i++) { // 空列表时不进入循环。
    var item = cells.get(i); // 下标从零开始。
    if (item != null) { // 手动构造的列表可能放入空项。
        log(item.getLabel() + ":" + item.getSimilar()); // 继续读取目标对象的成员。
    }
}
```


### setData(data)

> 替换目标列表。
> 
> 列表类型为 List<YoloResultCell>，每项是包含类别、分数和坐标的目标对象。
> setData 会复制两份列表容器，但不复制每个目标对象；之后修改输入列表的长度不影响保存列表，修改共享目标对象的字段则会影响读取结果。
> getData 返回内部英文列表本身，不是副本；对它增删会直接改变结果，不会同步中文列表。
> 输入不能为 null，否则构造复制列表时会抛出异常；可以传空列表。返回 void，无返回值，也不会更新成功状态。

- 参数 : data {List<YoloResultCell>} 非空引用的 Java 目标列表，可以没有元素
- 返回 : {void} 无返回值


```javascript
var result = new YoloResult(); // 构造教学结果，不会执行检测。
var cell = new YoloResultCell(); // 创建一条目标数据。
cell.setLabel("phone"); cell.setSimilar(0.92); // 填写类别和分数。
var list = new java.util.ArrayList(); // 创建 Java 列表，不是脚本数组。
list.add(cell); // 把目标对象放入列表。
result.setData(list); // 复制列表容器，目标对象仍由双方共享。
var cells = result.getData(); // 读取当前列表。
for (var i = 0; i < cells.size(); i++) { // 空列表时不进入循环。
    var item = cells.get(i); // 下标从零开始。
    if (item != null) { // 手动构造的列表可能放入空项。
        log(item.getLabel() + ":" + item.getSimilar()); // 继续读取目标对象的成员。
    }
}
list.clear(); // 清空原输入列表，不会清空保存的副本。
log(result.getData().size()); // 仍为一。
cell.setLabel("updated"); // 修改共享的目标对象。
log(result.getData().get(0).getLabel()); // 保存列表也能看到新标签。
```


### getErr()

> 读取错误说明。
> 
> 初始值为 “暂无异常”。文字允许为 null。
> 设置方法同时更新对应的中英文存储，但不会自动改变其他字段，也不会触发模型检测。
> 没有输入参数，返回 String 类型的当前英文存储值。

- 返回 : {String} 当前保存的错误说明


```javascript
var result = new YoloResult(); // 构造教学结果。
log(result.getErr()); // 查看初始值。
result.setErr("sample error"); // 设置这一项数据。
log(result.getErr()); // 查看设置后的值。
```


### setErr(err)

> 设置错误说明。
> 
> 初始值为 “暂无异常”。文字允许为 null。
> 设置方法同时更新对应的中英文存储，但不会自动改变其他字段，也不会触发模型检测。
> 输入类型为 String；返回 void，无返回值。

- 参数 : err {String} 要保存的错误说明
- 返回 : {void} 无返回值


```javascript
var result = new YoloResult(); // 构造教学结果。
log(result.getErr()); // 查看初始值。
result.setErr("sample error"); // 设置这一项数据。
log(result.getErr()); // 查看设置后的值。
```


### json()

> 生成英文键名的整体结果文本。
> 
> 没有输入参数，返回 String（字符串），不是脚本对象。两种输出都从英文存储字段和英文 data 列表读取。
> 当前通过拼接生成文本，没有转义说明、错误和目标标签中的引号或换行，因此并不保证任意内容都能作为合法 JSON 解析。
> 需要可靠保存任意文字时，应读取各项数据组成脚本对象，再用 JSON.stringify。

- 返回 : {String} 拼接得到的整体结果文本


```javascript
var result = new YoloResult(); // 构造教学结果，不会执行检测。
var cell = new YoloResultCell(); // 创建一条目标数据。
cell.setLabel("phone"); cell.setSimilar(0.92); // 填写类别和分数。
var list = new java.util.ArrayList(); // 创建 Java 列表，不是脚本数组。
list.add(cell); // 把目标对象放入列表。
result.setData(list); // 复制列表容器，目标对象仍由双方共享。
log(result.json()); // 查看包含目标项和状态的文本。
```


### json_zn()

> 生成中文键名的整体结果文本。
> 
> 没有输入参数，返回 String（字符串），不是脚本对象。两种输出都从英文存储字段和英文 data 列表读取。
> 当前通过拼接生成文本，没有转义说明、错误和目标标签中的引号或换行，因此并不保证任意内容都能作为合法 JSON 解析。
> 需要可靠保存任意文字时，应读取各项数据组成脚本对象，再用 JSON.stringify。
> 目标项通过 json_zn 输出；列表中若含 null，该方法会抛出异常。实际方法名就是 json_zn，没有另外的中文方法别名。

- 返回 : {String} 拼接得到的整体结果文本


```javascript
var 结果 = new YoloResult(); // 构造教学结果，不会执行检测。
var 目标 = new YoloResultCell(); // 创建一条目标数据。
目标.setLabel("手机"); 目标.setSimilar(0.92); // 填写类别和分数。
var 列表 = new java.util.ArrayList(); // 创建 Java 列表，不是脚本数组。
列表.add(目标); // 把目标对象放入列表。
结果.setData(列表); // 复制列表容器，目标对象仍由双方共享。
日志(结果.json_zn()); // 查看包含目标项和状态的文本。
```


