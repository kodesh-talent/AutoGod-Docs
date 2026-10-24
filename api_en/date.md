# $date - 日期工具

- 更新时间:2026-10-22 10:55:46

> 日期时间工具（脚本里的 $date 对象）。
> 



```javascript
var now = $date.dt();
```




### dt()

> 将日期时间整理为 yyyy-MM-dd HH:mm:ss 形式的文字。
> 输入：无参数，使用调用时的当前时间。
> 输出：String，格式化后的文字。
> 日期的拆分和显示使用设备默认时区；改变设备时区可能改变同一时间戳显示出的小时和日期。

- 返回 : {String} 得到的日期或时长文字；具体空值行为见说明
- 版本 : 1.1.4


```javascript
var result = $date.dt(); //调用当前重载
if (result != null) { //字符串解析失败时不能继续读取属性
    log("转换结果：" + result);
} else {
    log("未取得日期结果，请检查输入");
}
```


### dt(time)

> 将日期时间整理为 yyyy-MM-dd HH:mm:ss 形式的文字。
> 输入：long 毫秒时间戳。以协调世界时一九七零年一月一日零点为基准，不要把秒时间戳直接传入。
> 输出：String，格式化后的文字。
> 日期的拆分和显示使用设备默认时区；改变设备时区可能改变同一时间戳显示出的小时和日期。

- 参数 : time {long} 要处理的毫秒时间戳
- 返回 : {String} 得到的日期或时长文字；具体空值行为见说明
- 版本 : 1.1.4


```javascript
var timestamp = $date.curTime(); //先取得毫秒时间戳
var result = $date.dt(timestamp); //调用当前重载
if (result != null) { //字符串解析失败时不能继续读取属性
    log("转换结果：" + result);
} else {
    log("未取得日期结果，请检查输入");
}
```


### dt(time)

> 将日期时间整理为 yyyy-MM-dd HH:mm:ss 形式的文字。
> 输入：String 日期时间文字，建议按 yyyy-MM-dd HH:mm:ss 格式填写。解析失败时返回 null，不要传 null。
> 输出：String，格式化后的文字。
> 日期的拆分和显示使用设备默认时区；改变设备时区可能改变同一时间戳显示出的小时和日期。

- 参数 : time {String} 要解析的日期时间文字，例如 "2026-01-02 03:04:05"
- 返回 : {String} 得到的日期或时长文字；具体空值行为见说明
- 版本 : 1.1.4


```javascript
var result = $date.dt("2026-01-02 03:04:05"); //调用当前重载
if (result != null) { //字符串解析失败时不能继续读取属性
    log("转换结果：" + result);
} else {
    log("未取得日期结果，请检查输入");
}
```


### d()

> 将日期整理为 yyyy-MM-dd 形式的文字，不包含时间。
> 输入：无参数，使用调用时的当前时间。
> 输出：String，格式化后的文字。
> 日期的拆分和显示使用设备默认时区；改变设备时区可能改变同一时间戳显示出的小时和日期。

- 返回 : {String} 得到的日期或时长文字；具体空值行为见说明
- 版本 : 1.1.4


```javascript
var result = $date.d(); //调用当前重载
if (result != null) { //字符串解析失败时不能继续读取属性
    log("转换结果：" + result);
} else {
    log("未取得日期结果，请检查输入");
}
```


### d(time)

> 将日期整理为 yyyy-MM-dd 形式的文字，不包含时间。
> 输入：long 毫秒时间戳。以协调世界时一九七零年一月一日零点为基准，不要把秒时间戳直接传入。
> 输出：String，格式化后的文字。
> 日期的拆分和显示使用设备默认时区；改变设备时区可能改变同一时间戳显示出的小时和日期。

- 参数 : time {long} 要处理的毫秒时间戳
- 返回 : {String} 得到的日期或时长文字；具体空值行为见说明
- 版本 : 1.1.4


```javascript
var timestamp = $date.curTime(); //先取得毫秒时间戳
var result = $date.d(timestamp); //调用当前重载
if (result != null) { //字符串解析失败时不能继续读取属性
    log("转换结果：" + result);
} else {
    log("未取得日期结果，请检查输入");
}
```


### parse(dateStr, pattern)

> 把日期时间文字解析为宿主 Date 日期对象。
> 输入：String 日期文字和 String 模板。模板要与输入格式一致。
> 输出：java.util.Date 对象；通常的解析失败返回 null。日期文字不能为空，模板无效等参数错误仍可能抛出异常。
> 按设备默认时区解析。解析器允许一定的日期自动调整，也可能只解析输入开头，因此不要把返回非空当作严格的日期合法性校验。

- 参数 : dateStr {String} 要解析的非空日期文字
- 参数 : pattern {String} 匹配输入的日期模板，MM 表示月份，mm 表示分钟
- 返回 : {Date} 宿主日期对象；字符串解析失败时为 null
- 版本 : 1.1.4


```javascript
var result = $date.parse("2026-01-02 03:04:05", "yyyy-MM-dd HH:mm:ss"); //文字转成日期对象
if (result != null) {
    log("解析后：" + $date.format(result, "yyyy年MM月dd日 HH:mm:ss")); //换一个模板展示
} else {
    log("无法解析，请核对日期内容和模板");
}
```


### parse(dateStr)

> 把日期时间文字解析为宿主 Date 日期对象。
> 输入：String 日期文字，内部会依次尝试预置格式，建议使用 yyyy-MM-dd HH:mm:ss 这样的明确格式。
> 输出：java.util.Date 对象；通常的解析失败返回 null。日期文字不能为空，模板无效等参数错误仍可能抛出异常。
> 按设备默认时区解析。解析器允许一定的日期自动调整，也可能只解析输入开头，因此不要把返回非空当作严格的日期合法性校验。

- 参数 : dateStr {String} 要解析的非空日期文字
- 返回 : {Date} 宿主日期对象；字符串解析失败时为 null
- 版本 : 1.1.4


```javascript
var result = $date.parse("2026-01-02 03:04:05"); //文字转成日期对象
if (result != null) {
    log("解析后：" + $date.format(result, "yyyy年MM月dd日 HH:mm:ss")); //换一个模板展示
} else {
    log("无法解析，请核对日期内容和模板");
}
```


### info()

> 把一个时刻拆成年、月、日、星期和时间等信息。
> 输入：无参数，使用调用时的当前时间。
> 输出：DateInfo，日期信息快照，可直接读取字段，也可以调用对应的读取方法。
> 日期的拆分和显示使用设备默认时区；改变设备时区可能改变同一时间戳显示出的小时和日期。
> 月份是一到十二；星期编号一代表星期日。快照不会自动随时间更新，中英文字段也不要手动修改后期望互相同步。

- 返回 : {DateInfo} 日期信息快照；字符串解析失败时为 null
- 版本 : 1.1.4


```javascript
var result = $date.info(); //调用当前重载
if (result != null) { //字符串解析失败时不能继续读取属性
    log("日期：" + result.year + "-" + result.month + "-" + result.day);
    log("时间：" + result.hour + ":" + result.min + ":" + result.sec);
    log("星期编号：" + result.week); //一表示星期日，七表示星期六
    log("时间戳：" + result.getStamp()); //演示返回对象的读取方法
} else {
    log("未取得日期结果，请检查输入");
}
```


### info(time)

> 把一个时刻拆成年、月、日、星期和时间等信息。
> 输入：long 毫秒时间戳。以协调世界时一九七零年一月一日零点为基准，不要把秒时间戳直接传入。
> 输出：DateInfo，日期信息快照，可直接读取字段，也可以调用对应的读取方法。
> 日期的拆分和显示使用设备默认时区；改变设备时区可能改变同一时间戳显示出的小时和日期。
> 月份是一到十二；星期编号一代表星期日。快照不会自动随时间更新，中英文字段也不要手动修改后期望互相同步。

- 参数 : time {long} 要处理的毫秒时间戳
- 返回 : {DateInfo} 日期信息快照；字符串解析失败时为 null
- 版本 : 1.1.4


```javascript
var timestamp = $date.curTime(); //先取得毫秒时间戳
var result = $date.info(timestamp); //调用当前重载
if (result != null) { //字符串解析失败时不能继续读取属性
    log("日期：" + result.year + "-" + result.month + "-" + result.day);
    log("时间：" + result.hour + ":" + result.min + ":" + result.sec);
    log("星期编号：" + result.week); //一表示星期日，七表示星期六
    log("时间戳：" + result.getStamp()); //演示返回对象的读取方法
} else {
    log("未取得日期结果，请检查输入");
}
```


### info(time)

> 把一个时刻拆成年、月、日、星期和时间等信息。
> 输入：String 日期时间文字，建议按 yyyy-MM-dd HH:mm:ss 格式填写。解析失败时返回 null，不要传 null。
> 输出：DateInfo，日期信息快照，可直接读取字段，也可以调用对应的读取方法。
> 日期的拆分和显示使用设备默认时区；改变设备时区可能改变同一时间戳显示出的小时和日期。
> 月份是一到十二；星期编号一代表星期日。快照不会自动随时间更新，中英文字段也不要手动修改后期望互相同步。

- 参数 : time {String} 要解析的日期时间文字，例如 "2026-01-02 03:04:05"
- 返回 : {DateInfo} 日期信息快照；字符串解析失败时为 null
- 版本 : 1.1.4


```javascript
var result = $date.info("2026-01-02 03:04:05"); //调用当前重载
if (result != null) { //字符串解析失败时不能继续读取属性
    log("日期：" + result.year + "-" + result.month + "-" + result.day);
    log("时间：" + result.hour + ":" + result.min + ":" + result.sec);
    log("星期编号：" + result.week); //一表示星期日，七表示星期六
    log("时间戳：" + result.getStamp()); //演示返回对象的读取方法
} else {
    log("未取得日期结果，请检查输入");
}
```


### format(time, pattern)

> 按指定模板把日期变成文字。
> 输入：long 日期值和 String 输出模板；模板中的 yyyy 是年份，MM 是月份，dd 是日期，HH 是二十四小时，mm 是分钟，ss 是秒。
> 输出：String 格式化文字，显示时使用设备默认时区。模板不是普通说明文字，月份和分钟的字母大小写不能混用。
> 日期对象或模板为 null 时可能返回 null；日期字符串解析失败返回 null，无效模板可能抛出异常。

- 参数 : time {long} 毫秒时间戳，不是秒数
- 参数 : pattern {String} 输出模板，如 "yyyy-MM-dd HH:mm:ss"
- 返回 : {String} 得到的日期或时长文字；具体空值行为见说明
- 版本 : 1.1.4


```javascript
var timestamp = $date.curTime(); //单位是毫秒
var result = $date.format(timestamp, "yyyy年MM月dd日 HH:mm:ss"); //按模板输出
log("显示文字：" + result);
```


### format(date, pattern)

> 按指定模板把日期变成文字。
> 输入：Date 日期值和 String 输出模板；模板中的 yyyy 是年份，MM 是月份，dd 是日期，HH 是二十四小时，mm 是分钟，ss 是秒。
> 输出：String 格式化文字，显示时使用设备默认时区。模板不是普通说明文字，月份和分钟的字母大小写不能混用。
> 日期对象或模板为 null 时可能返回 null；日期字符串解析失败返回 null，无效模板可能抛出异常。

- 参数 : date {Date} 宿主 java.util.Date 日期对象，可由日期工具创建
- 参数 : pattern {String} 输出模板，如 "yyyy-MM-dd HH:mm:ss"
- 返回 : {String} 得到的日期或时长文字；具体空值行为见说明
- 版本 : 1.1.4


```javascript
var dateValue = $date.date(); //获取宿主日期对象
var result = $date.format(dateValue, "yyyy年MM月dd日 HH:mm:ss"); //按模板输出
log("显示文字：" + result);
```


### format(dateStr, pattern)

> 按指定模板把日期变成文字。
> 输入：String 日期值和 String 输出模板；模板中的 yyyy 是年份，MM 是月份，dd 是日期，HH 是二十四小时，mm 是分钟，ss 是秒。
> 输出：String 格式化文字，显示时使用设备默认时区。模板不是普通说明文字，月份和分钟的字母大小写不能混用。
> 日期对象或模板为 null 时可能返回 null；日期字符串解析失败返回 null，无效模板可能抛出异常。

- 参数 : dateStr {String} 按预置格式解析的日期文字，不能传空对象
- 参数 : pattern {String} 输出模板，如 "yyyy-MM-dd HH:mm:ss"
- 返回 : {String} 得到的日期或时长文字；具体空值行为见说明
- 版本 : 1.1.4


```javascript
var result = $date.format("2026-01-02 03:04:05", "yyyy年MM月dd日 HH:mm:ss"); //按模板输出
log("显示文字：" + result);
```


### date()

> 创建宿主的 java.util.Date 日期对象。
> 输入：无参数，使用调用时的当前时间。
> 输出：Date，宿主日期对象，不是脚本内置日期构造器创建的对象；可继续交给日期工具格式化。
> 日期的拆分和显示使用设备默认时区；改变设备时区可能改变同一时间戳显示出的小时和日期。

- 返回 : {Date} 宿主日期对象；字符串解析失败时为 null
- 版本 : 1.1.4


```javascript
var result = $date.date(); //调用当前重载
if (result != null) { //字符串解析失败时不能继续读取属性
    log("日期文字：" + $date.format(result, "yyyy-MM-dd HH:mm:ss")); //继续使用返回的日期对象
} else {
    log("未取得日期结果，请检查输入");
}
```


### date(time)

> 创建宿主的 java.util.Date 日期对象。
> 输入：long 毫秒时间戳。以协调世界时一九七零年一月一日零点为基准，不要把秒时间戳直接传入。
> 输出：Date，宿主日期对象，不是脚本内置日期构造器创建的对象；可继续交给日期工具格式化。
> 日期的拆分和显示使用设备默认时区；改变设备时区可能改变同一时间戳显示出的小时和日期。

- 参数 : time {long} 要处理的毫秒时间戳
- 返回 : {Date} 宿主日期对象；字符串解析失败时为 null
- 版本 : 1.1.4


```javascript
var timestamp = $date.curTime(); //先取得毫秒时间戳
var result = $date.date(timestamp); //调用当前重载
if (result != null) { //字符串解析失败时不能继续读取属性
    log("日期文字：" + $date.format(result, "yyyy-MM-dd HH:mm:ss")); //继续使用返回的日期对象
} else {
    log("未取得日期结果，请检查输入");
}
```


### date(dateStr)

> 创建宿主的 java.util.Date 日期对象。
> 输入：String 日期时间文字，建议按 yyyy-MM-dd HH:mm:ss 格式填写。解析失败时返回 null，不要传 null。
> 输出：Date，宿主日期对象，不是脚本内置日期构造器创建的对象；可继续交给日期工具格式化。
> 日期的拆分和显示使用设备默认时区；改变设备时区可能改变同一时间戳显示出的小时和日期。

- 参数 : dateStr {String} 要解析的日期时间文字，例如 "2026-01-02 03:04:05"
- 返回 : {Date} 宿主日期对象；字符串解析失败时为 null
- 版本 : 1.1.4


```javascript
var result = $date.date("2026-01-02 03:04:05"); //调用当前重载
if (result != null) { //字符串解析失败时不能继续读取属性
    log("日期文字：" + $date.format(result, "yyyy-MM-dd HH:mm:ss")); //继续使用返回的日期对象
} else {
    log("未取得日期结果，请检查输入");
}
```


### dur(milliseconds)

> 把一段持续时间换算成天、时、分、秒的中文文字。
> 输入：Number 数值，单位为毫秒；这是持续时长，不是日期时间戳。内部先取整数毫秒，再舍去不足一秒的部分。
> 输出：String 字符串；零或负值得到 "0秒"，正数不足一秒也得到 "0秒"，传 null 得到文字 "null"。
> 结果省略数值为零的单位，一天按二十四小时计算，不受时区影响。

- 参数 : milliseconds {Number} 要换算的毫秒时长；小数部分会被舍去
- 返回 : {String} 得到的日期或时长文字；具体空值行为见说明
- 版本 : 1.6.1


```javascript
var result = $date.dur(90061000); //一天一小时一分钟一秒
log("时长：" + result); //得到“1天1时1分1秒”
log("不足一秒：" + $date.dur(500)); //得到“0秒”
log("没有时长：" + $date.dur(0)); //得到“0秒”
```


### curTime()

> 读取当前系统时间的毫秒时间戳。
> 输入：无参数。输出：long 长整数，以协调世界时一九七零年一月一日零点为基准。
> 同一时刻的时间戳不随显示时区改变；系统时间被用户或网络校准时可能跳变，不适合作为保证单调递增的计时器。

- 返回 : {long} 当前系统时间的毫秒时间戳
- 版本 : 1.7.8


```javascript
var result = $date.curTime(); //读取当前毫秒时间戳
log("毫秒时间戳：" + result);
log("本地显示：" + $date.format(result, "yyyy-MM-dd HH:mm:ss")); //按设备时区转为文字
```


