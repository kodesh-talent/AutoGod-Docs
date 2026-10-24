# 

- 更新时间:2026-10-22 10:55:46

> 加密、解密和摘要运算的配置对象。
> 
> input 决定怎样理解输入，output 决定怎样呈现输出，encoding 用于文字和字节转换。type 只在相关密钥构造中使用，dest 的当前行为需查看字段说明。
> 可以用普通脚本对象填写选项，也可以新建 CryptOptions。运算之间的默认处理不完全相同，建议明确填写输入、输出和编码。
> 下面演示摘要运算及配置传递；摘要不是可还原原文的加密结果。



```javascript
var options = { input: "string", output: "hex", encoding: "utf-8" };
try {
    var result = $crypt.digest("教学文本", "SHA-256", options);
    log(result); // 返回十六进制文本，供后续脚本使用。
} catch (error) {
    log("摘要运算失败：" + error);
}
```




### const {String} input;

> 输入数据格式。
> 
> 字段类型为 String（字符串）。默认是 string，表示把普通文字按 encoding 转成字节。base64 和 hex 表示先解码相应字符串，bytes 表示输入 Java 字节数组，file 表示读取文件路径。
> 不要把编码后的文字当作普通文字，也不要把普通脚本数字数组当作 Java 字节数组。


```javascript
try {
    var options = { input: "hex", output: "hex", encoding: "utf-8" };
    // 十六进制 616263 表示三个字节，对应普通文字 abc。
    var result = $crypt.digest("616263", "SHA-256", options);
    log(result); // 结果是摘要的十六进制字符串。
} catch (error) {
    log("配置示例执行失败：" + error);
}
```


### const {String} output;

> 输出结果格式。
> 
> 字段类型为 String（字符串）。默认是 hex，表示十六进制字符串；base64 输出编码字符串，bytes 输出 Java 字节数组，string 按 encoding 把结果字节转换成文字。
> 加密结果通常不是可读文字，只有确实表示文字的字节才适合 string。未识别的输出格式在通用输出转换中按十六进制处理。


```javascript
try {
    var options = { input: "string", output: "bytes", encoding: "utf-8" };
    var bytes = $crypt.digest("教学文本", "SHA-256", options);
    log("结果字节数：" + bytes.length); // Java 数组用 length 读取长度。
} catch (error) {
    log("配置示例执行失败：" + error);
}
```


### const {String} dest;

> 期望写入的目标路径。
> 
> 字段类型为 String（字符串）。类型为 String，初始为 null。此字段用于加解密内部的文件输出分支，不是所有运算都会使用的通用保存路径。
> 当前文件输出条件在目标路径为空且 output 为 file 时才进入文件流分支，可能因此失败；填写非空路径反而不会走这个分支。不要认为只填此字段就能可靠地保存结果，摘要和通用输出转换也不会据此写文件。


```javascript
try {
    var options = new CryptOptions();
    options.dest = "/sdcard/crypt-result.dat"; // 只演示设置字段，不执行文件写入。
    log(options.dest); // 保存了路径文字，并不代表文件已经创建。
} catch (error) {
    log("配置示例执行失败：" + error);
}
```


### const {String} type;

> 密钥类型标记。
> 
> 字段类型为 String（字符串）。类型为 String，初始为 null。public 表示公钥，private 表示私钥；CryptKey 的带配置构造方法会读取此值。
> 它不控制文本输入输出，也不会把任意字节变成有效密钥。传给摘要或加解密的运算配置，不会自动改写已经存在的 CryptKey 类型。


```javascript
try {
    var pair = $crypt.generateKeyPair("RSA", 2048);
    var options = new CryptOptions();
    options.type = "public"; // 与下面复制的公钥编码对应。
    var key = new CryptKey(pair.getPublicKey().getData(), options);
    log(key.getType()); // 只查看类型，不输出密钥内容。
} catch (error) {
    log("配置示例执行失败：" + error);
}
```


### const {String} encoding;

> 文字和字节之间转换的字符编码。
> 
> 字段类型为 String（字符串）。类型为 String，默认 utf-8。普通文字输入及 string 输出会使用这个编码。
> 它不是密钥算法名，也不是 base64 或 hex 格式。中文文字建议明确填写 utf-8；无效编码可能使转换失败。


```javascript
try {
    var options = { input: "string", output: "hex", encoding: "utf-8" };
    var result = $crypt.digest("中文教学文本", "SHA-256", options);
    log(result); // 对按指定编码转换后的字节求摘要。
} catch (error) {
    log("配置示例执行失败：" + error);
}
```


