# Ws - WS封装对象

- 更新时间:2026-10-22 10:55:52

> 双向长连接的脚本包装对象，由 $ws.create 或 $通信.创建 返回。
> 得到对象只表示连接已发起，不表示已经连上。拿到后应立即注册需要的监听，发送可放到打开回调中。
> 当前创建方法先启动网络连接再返回对象，极早发生的事件可能早于自定义监听注册；监听不会补发过去的事件。
> 回调中的连接参数是 okhttp3.WebSocket，和这里的 Ws 包装对象不同；底层方法仍使用英文名字。



```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的长连接服务
socket.onFail(function (error, response, raw) {
    log("连接失败：" + error.getMessage());
});
socket.onMsgStr(function (text, raw) {
    log("收到文字：" + text);
});
socket.onOpen(function (response, raw) {
    raw.send("你好服务器"); //通过回调参数发送，避免依赖外部变量的赋值时机
});
```




### send(msg)

> 向当前连接提交文字消息。
> 输出：void，没有返回数据。调用结束不表示服务器已经收到消息或连接已经关闭。
> 输入：String，不要传 null。当前包装方法没有保留底层发送的布尔结果，不能通过返回值判断发送是否成功。
> 示例在打开回调中发送；如果需要确认业务处理结果，应由服务器返回对应的确认消息。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : msg {String} 要发送的消息数据，格式和转换规则见说明


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onOpen(function (response, raw) {
    socket.send("你好服务器"); //发送文字消息，不会自动把它转换成对象数据
});
```


### send(bytes)

> 向当前连接提交二进制消息。
> 输出：void，没有返回数据。调用结束不表示服务器已经收到消息或连接已经关闭。
> 输入：byte[]，不要传 null。当前包装方法没有保留底层发送的布尔结果，不能通过返回值判断发送是否成功。
> 示例在打开回调中发送；如果需要确认业务处理结果，应由服务器返回对应的确认消息。
> byte[] 是宿主字节数组，元素使用有符号字节值。示例用反射创建明确的数组类型，避免多个发送重载对普通数组产生歧义。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : bytes {byte[]} 要发送的消息数据，格式和转换规则见说明


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onOpen(function (response, raw) {
    var bytes = java.lang.reflect.Array.newInstance(java.lang.Byte.TYPE, 3); //创建三个字节的位置
    bytes[0] = 65; //第一个字节
    bytes[1] = 66; //第二个字节
    bytes[2] = 67; //第三个字节
    socket.send(bytes); //按二进制发送，不是文字消息
});
```


### send(byteString)

> 向当前连接提交二进制消息。
> 输出：void，没有返回数据。调用结束不表示服务器已经收到消息或连接已经关闭。
> 输入：ByteString，不要传 null。当前包装方法没有保留底层发送的布尔结果，不能通过返回值判断发送是否成功。
> 示例在打开回调中发送；如果需要确认业务处理结果，应由服务器返回对应的确认消息。
> ByteString 是 okio 提供的字节串类型。示例通过 Packages 访问宿主类，把文字编码成 UTF-8 字节串后发送。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : byteString {ByteString} 要发送的消息数据，格式和转换规则见说明


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onOpen(function (response, raw) {
    var data = Packages.okio.ByteString.encodeUtf8("你好"); //得到 ByteString 对象
    socket.send(data); //发送字节串
});
```


### sendBase64(base64Str)

> 向当前连接提交二进制消息。
> 输出：void，没有返回数据。调用结束不表示服务器已经收到消息或连接已经关闭。
> 输入：String，不要传 null。当前包装方法没有保留底层发送的布尔结果，不能通过返回值判断发送是否成功。
> 示例在打开回调中发送；如果需要确认业务处理结果，应由服务器返回对应的确认消息。
> 参数是 Base64 编码文字，发送前会解码；发送的是解码后的字节，并不是这段编码文字。解码结果为空时只记录错误并返回。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : base64Str {String} 要发送的消息数据，格式和转换规则见说明


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onOpen(function (response, raw) {
    socket.sendBase64("QUJD"); //解码为三个字节后发送
});
```


### sendHex(hexStr)

> 向当前连接提交二进制消息。
> 输出：void，没有返回数据。调用结束不表示服务器已经收到消息或连接已经关闭。
> 输入：String，不要传 null。当前包装方法没有保留底层发送的布尔结果，不能通过返回值判断发送是否成功。
> 示例在打开回调中发送；如果需要确认业务处理结果，应由服务器返回对应的确认消息。
> 十六进制每两个字符代表一个字节，只使用零到九和大小写 A 到 F，长度应为偶数；不要加空格或前缀。非法输入可能抛出异常。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : hexStr {String} 要发送的消息数据，格式和转换规则见说明


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onOpen(function (response, raw) {
    socket.sendHex("414243"); //三个字节，分别是十六进制四一、四二、四三
});
```


### cancel()

> 立即取消这条连接。
> 输出：void，没有返回数据。调用结束不表示服务器已经收到消息或连接已经关闭。
> 输入：无参数。cancel()、stop()、不带参数的 close() 都调用底层取消操作，不进行正常关闭握手。
> 尚未发送的数据可能被丢弃；后续通知可能进入失败回调。需要正常关闭请使用带关闭码的重载。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.cancel(); //本例立即取消刚发起的连接，用来演示取消操作
```


### stop()

> 立即取消这条连接。
> 输出：void，没有返回数据。调用结束不表示服务器已经收到消息或连接已经关闭。
> 输入：无参数。cancel()、stop()、不带参数的 close() 都调用底层取消操作，不进行正常关闭握手。
> 尚未发送的数据可能被丢弃；后续通知可能进入失败回调。需要正常关闭请使用带关闭码的重载。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.stop(); //本例立即取消刚发起的连接，用来演示取消操作
```


### close()

> 立即取消这条连接。
> 输出：void，没有返回数据。调用结束不表示服务器已经收到消息或连接已经关闭。
> 输入：无参数。cancel()、stop()、不带参数的 close() 都调用底层取消操作，不进行正常关闭握手。
> 尚未发送的数据可能被丢弃；后续通知可能进入失败回调。需要正常关闭请使用带关闭码的重载。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.close(); //本例立即取消刚发起的连接，用来演示取消操作
```


### close(code)

> 发起正常关闭握手。
> 输出：void，没有返回数据。调用结束不表示服务器已经收到消息或连接已经关闭。
> 输入：int 关闭码，本重载使用空原因文字。
> 正常结束通常使用 1000；非法关闭码或过长原因可能抛出异常。这里只提交关闭请求，实际完成请等待关闭回调。
> 这与不带参数的关闭方法不同：不带参数会直接取消连接。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : code {int} 关闭状态码，示例用 1000 表示正常结束


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onOpen(function (response, raw) {
    socket.close(1000); //本例在打开后马上请求正常关闭
});
```


### close(code, reason)

> 发起正常关闭握手。
> 输出：void，没有返回数据。调用结束不表示服务器已经收到消息或连接已经关闭。
> 输入：int 关闭码和 String 关闭原因。原因传 null 时会按空字符串处理。
> 正常结束通常使用 1000；非法关闭码或过长原因可能抛出异常。这里只提交关闭请求，实际完成请等待关闭回调。
> 这与不带参数的关闭方法不同：不带参数会直接取消连接。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : code {int} 关闭状态码，示例用 1000 表示正常结束
- 参数 : reason {String} 简短关闭原因；null 按空字符串处理


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onOpen(function (response, raw) {
    socket.close(1000, "示例结束"); //本例在打开后马上请求正常关闭
});
```


### onMsgByte(callback)

> 设置“收到二进制消息”时执行的回调。
> 输入：WsOnMessageBS 接口，可传普通脚本函数。回调依次收到 ByteString 字节串；只有一个参数，没有连接参数。
> 输出：Ws，返回当前包装对象本身，不是回调执行结果；回调自己的输出为 void，无需返回数据。
> 同类监听再次设置会替换之前的函数；传 null 会停用该类回调，不会恢复默认日志。
> 回调由网络事件触发，可能在后台线程执行；操作界面请用 $thread.ui 或 $线程.界面。
> 底层参数没有本包装类的中文别名，调用它们的方法时保留原来的英文名称。
> ByteString 不是脚本普通数组；用 size() 读取长度，用 toByteArray() 取得 byte[]。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : callback {WsOnMessageBS} 收到二进制消息时执行的函数，参数顺序和类型见说明；可传 null
- 返回 : {Ws} 当前连接包装对象，可继续设置其他监听


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onMsgByte(function (data) {
    log("字节数量：" + data.size()); //先查看长度
    var bytes = data.toByteArray(); //转成宿主 byte[] 数组
    if (bytes.length > 0) {
        log("首字节：" + (bytes[0] & 255)); //转换为零到二百五十五的数值
    }
});
```


### onMsgStr(callback)

> 设置“收到文字消息”时执行的回调。
> 输入：WsOnMessageStr 接口，可传普通脚本函数。回调依次收到 String 文字和 okhttp3.WebSocket 底层连接。
> 输出：Ws，返回当前包装对象本身，不是回调执行结果；回调自己的输出为 void，无需返回数据。
> 同类监听再次设置会替换之前的函数；传 null 会停用该类回调，不会恢复默认日志。
> 回调由网络事件触发，可能在后台线程执行；操作界面请用 $thread.ui 或 $线程.界面。
> 底层参数没有本包装类的中文别名，调用它们的方法时保留原来的英文名称。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : callback {WsOnMessageStr} 收到文字消息时执行的函数，参数顺序和类型见说明；可传 null
- 返回 : {Ws} 当前连接包装对象，可继续设置其他监听


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onMsgStr(function (text, raw) {
    log("收到文字：" + text); //文字不一定是对象数据，先按字符串处理
});
```


### onOpen(callback)

> 设置“连接握手成功”时执行的回调。
> 输入：WsOnOpen 接口，可传普通脚本函数。回调依次收到 okhttp3.Response 握手响应和 okhttp3.WebSocket 底层连接。
> 输出：Ws，返回当前包装对象本身，不是回调执行结果；回调自己的输出为 void，无需返回数据。
> 同类监听再次设置会替换之前的函数；传 null 会停用该类回调，不会恢复默认日志。
> 回调由网络事件触发，可能在后台线程执行；操作界面请用 $thread.ui 或 $线程.界面。
> 底层参数没有本包装类的中文别名，调用它们的方法时保留原来的英文名称。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : callback {WsOnOpen} 连接握手成功时执行的函数，参数顺序和类型见说明；可传 null
- 返回 : {Ws} 当前连接包装对象，可继续设置其他监听


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onOpen(function (response, raw) {
    log("握手状态码：" + response.code()); //这是底层响应，不是 HttpResponse
    var accepted = raw.send("你好服务器"); //底层发送方法有布尔返回值
    log("是否进入发送队列：" + accepted); //进入队列不代表服务器已处理
});
```


### onClosed(callback)

> 设置“连接完成正常关闭”时执行的回调。
> 输入：WsOnClosed 接口，可传普通脚本函数。回调依次收到 int 关闭码、String 关闭原因和 okhttp3.WebSocket 底层连接。
> 输出：Ws，返回当前包装对象本身，不是回调执行结果；回调自己的输出为 void，无需返回数据。
> 同类监听再次设置会替换之前的函数；传 null 会停用该类回调，不会恢复默认日志。
> 回调由网络事件触发，可能在后台线程执行；操作界面请用 $thread.ui 或 $线程.界面。
> 底层参数没有本包装类的中文别名，调用它们的方法时保留原来的英文名称。
> 异常断网或主动取消可能走失败通知，不能保证所有退出方式都会触发这个正常关闭回调。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : callback {WsOnClosed} 连接完成正常关闭时执行的函数，参数顺序和类型见说明；可传 null
- 返回 : {Ws} 当前连接包装对象，可继续设置其他监听


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onClosed(function (code, reason, raw) {
    log("关闭码：" + code);
    log("关闭原因：" + reason); //此时不要再发送消息
});
```


### onClosing(callback)

> 设置“收到对方关闭请求”时执行的回调。
> 输入：WsOnClosing 接口，可传普通脚本函数。回调依次收到 int 关闭码、String 关闭原因和 okhttp3.WebSocket 底层连接。
> 输出：Ws，返回当前包装对象本身，不是回调执行结果；回调自己的输出为 void，无需返回数据。
> 同类监听再次设置会替换之前的函数；传 null 会停用该类回调，不会恢复默认日志。
> 回调由网络事件触发，可能在后台线程执行；操作界面请用 $thread.ui 或 $线程.界面。
> 底层参数没有本包装类的中文别名，调用它们的方法时保留原来的英文名称。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : callback {WsOnClosing} 收到对方关闭请求时执行的函数，参数顺序和类型见说明；可传 null
- 返回 : {Ws} 当前连接包装对象，可继续设置其他监听


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onClosing(function (code, reason, raw) {
    log("对方请求关闭：" + code + "，" + reason);
    raw.close(1000, "收到关闭通知"); //用底层方法回应关闭，等待最终关闭事件
});
```


### onFail(onFailure)

> 设置“连接失败或异常中断”时执行的回调。
> 输入：WsOnFailure 接口，可传普通脚本函数。回调依次收到 Throwable 异常、可能为 null 的 okhttp3.Response 响应、okhttp3.WebSocket 底层连接。
> 输出：Ws，返回当前包装对象本身，不是回调执行结果；回调自己的输出为 void，无需返回数据。
> 同类监听再次设置会替换之前的函数；传 null 会停用该类回调，不会恢复默认日志。
> 回调由网络事件触发，可能在后台线程执行；操作界面请用 $thread.ui 或 $线程.界面。
> 底层参数没有本包装类的中文别名，调用它们的方法时保留原来的英文名称。
> 失败响应可能为空，读取状态码前必须判断。失败通知不等同于正常关闭完成通知。
> 创建连接后要立即注册监听；当前实现没有回放机制，注册前发生的事件可能错过。示例地址仅展示格式，需要替换。

- 参数 : onFailure {WsOnFailure} 连接失败或异常中断时执行的函数，参数顺序和类型见说明；可传 null
- 返回 : {Ws} 当前连接包装对象，可继续设置其他监听


```javascript
var socket = $ws.create("wss://example.com/socket"); //替换成自己的服务器地址
socket.onFail(function (error, response, raw) {
    log("连接失败：" + error.getMessage()); //读取宿主异常对象的说明
    if (response != null) { //无网络等情况可能没有握手响应
        log("响应状态码：" + response.code());
    }
});
```


