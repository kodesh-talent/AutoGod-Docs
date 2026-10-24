# $str - 字符串操作

- 更新时间:2026-10-22 10:55:51

> 字符串处理工具（脚本里的 $str 对象）。
> 



```javascript
var encoded = $str.encodeBase64("hello");
var bytes = $str.getBytes("hello", "UTF-8");
```




### getBytes(str, encoding)

> 转字节(指定编码)

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : encoding {string} 字符编码名称，如 "UTF-8"、"GBK"；传 null 表示使用默认编码
- 返回 : {byte[]} 得到字符串对应的字节数组；字符串为空时返回 null
- 版本 : 1.0.0


```javascript
var strBytes = $str.getBytes("字符串","utf-8");
log("字节数组",strBytes);
```


### getBytes(str)

> 转字节

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {byte[]} 得到字符串对应的字节数组；字符串为空时返回 null
- 版本 : 1.0.0


```javascript
var strBytes = $str.getBytes("字符串");
log("字节数组",strBytes);
```


### extractNumbers(str)

> 提取数字
> 
> 将提取出来的数字使用','号分割，返回一个这样的字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 把提取到的多段数字用逗号 "," 连接成的字符串（没有数字时返回空串）
- 版本 : 1.0.0


```javascript
var nums = $str.extractNumbers("22字符33串44");
alert("提取数字",nums);
```


### decodeBase64(str, encoding)

> 把一段 Base64 编码的文本解码，还原成原来的字符串。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : encoding {string} 字符编码名称，如 "UTF-8"、"GBK"；传 null 表示使用默认编码
- 返回 : {string} 解码后的原始字符串；入参为空或编码不支持时返回 null
- 版本 : 1.0.0


```javascript
// （示例步骤）
var base64Str = $str.encodeBase64("我是字符串","utf-8");
// （示例步骤）
var str = $str.decodeBase64(base64Str,"utf-8");
alert("base64字符串",str);
```


### decodeBase64(str)

> 把一段 Base64 编码的文本解码，还原成原来的字符串。
> 
> 原字符串不会被修改，方法会返回一个新字符串；传入 null 时按各方法约定处理。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 解码后的原始字符串；入参为空或编码不支持时返回 null
- 版本 : 1.0.0


```javascript
// （示例步骤）
var base64Str = $str.encodeBase64("我是字符串");
// （示例步骤）
var str = $str.decodeBase64(base64Str);
alert("base64字符串",str);
```


### encodeBase64(str, encoding)

> 把字符串编码成 Base64 文本（常用于把中文或二进制安全地放进网址、接口里）。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : encoding {string} 字符编码名称，如 "UTF-8"、"GBK"；传 null 表示使用默认编码
- 返回 : {string} Base64 编码后的字符串；入参为空时返回 null
- 版本 : 1.0.0


```javascript
var base64Str = $str.encodeBase64("我是字符串","utf-8");
alert("base64字符串",base64Str);
```


### encodeBase64(str)

> 把字符串编码成 Base64 文本（常用于把中文或二进制安全地放进网址、接口里）。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} Base64 编码后的字符串；入参为空时返回 null
- 版本 : 1.0.0


```javascript
var base64Str = $str.encodeBase64("我是字符串","utf-8");
alert("base64字符串",base64Str);
```


### strToHex(str)

> 字符串转16进制

- 参数 : str {String} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {String} 每字节对应的两位十六进制字符串
- 版本 : 1.9.7


```javascript
var str = $str.strToHex("我是字符串");
log("16进制字符串:",str);
```


### hexToStr(dexStr)

> 16进制转字符串

- 参数 : dexStr {String} 要还原成文字的十六进制字符串（由 0-9、a-f/A-F 组成）
- 返回 : {String} 十六进制还原出的原始字符串；入参为空时返回 null
- 版本 : 1.9.7


```javascript
var src = $str.hexToStr("e68891e698afe5ad97e7aca6e4b8b2");
log("原字符串:",src);//我是字符串
```


### uriEncode(str)

> 对字符串做 URL 编码：把中文、空格等不安全字符转成 % 开头的形式，拼接网址参数时常用。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} URL 编码后的字符串；入参为 null 时返回 null
- 版本 : 1.3.7


```javascript
var result = $str.uriEncode("sample");
```


### uriDecode(str)

> 把 URL 编码过的字符串还原成原始内容。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} URL 解码还原出的原始字符串；入参为 null 时返回 null
- 版本 : 1.3.7


```javascript
var result = $str.uriDecode("sample");
```


### random(str)

> 随机字符

- 参数 : str {string]} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 随机取出的一个字符或列表中随机一项；入参为空时返回 null
- 版本 : 1.0.0


```javascript
//在输入的字符串中随机获取某个字符
for (var i = 0; i < 20; i++) {
    var str = $str.random("abcdefghijk");
    log(str);
}
```


### random(strList)

> 随机字符表

- 参数 : strList {string[]} 候选字符串列表，从中随机取一个
- 返回 : {string} 随机取出的一个字符或列表中随机一项；入参为空时返回 null
- 版本 : 1.0.0


```javascript
//在输入的字符列表中随机获取某个元素
for (var i = 0; i < 20; i++) {
    var str = $str.random(["abc","defg","hijk"]);
    log(str);
}
```


### isBlank(str)

> 是否为空白

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {boolean} true 表示是空白（null、空串或全是空格），false 表示不是
- 版本 : 1.0.0


```javascript
log($str.isBlank("    a "));//false
log($str.isBlank("     "));//true
```


### isNotBlank(str)

> 是否不是空白

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {boolean} true 表示有实际内容，false 表示是空白
- 版本 : 1.0.0


```javascript
log($str.isNotBlank("    a "));//true
log($str.isNotBlank("     "));//false
```


### hasBlank(strs)

> 字符数组是否有空白

- 参数 : strs {string[]} 字符串列表
- 返回 : {boolean} 列表里只要有任意一项是空白就返回 true
- 版本 : 1.0.0


```javascript
log($str.hasBlank(["    a ","  "]));//true
log($str.hasBlank(["    a "," b "]));//false
```


### isAllBlank(strs)

> 字符数组是否全是空白
> 
> 列表为 null 或空时，也会返回 true。

- 参数 : strs {string[]} 字符串列表
- 返回 : {boolean} 列表为空、null、或每一项都是空白时返回 true
- 版本 : 1.0.0


```javascript
log($str.isAllBlank(["    a ","  "]));//false
log($str.isAllBlank(["      ","  "]));//true
```


### isEmpty(str)

> 是否为空
> 
> 注意：纯空格也算作空；这是和 isBlank 配合使用的判断。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {boolean} true 表示为空（null、空串或纯空格），false 表示有内容
- 版本 : 1.0.0


```javascript
log($str.isEmpty("a "));//false
log($str.isEmpty("  "));//true
log($str.isEmpty(null));//true
```


### isNotEmpty(str)

> 是否不为空

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {boolean} true 表示有内容，false 表示为空
- 版本 : 1.0.0


```javascript
log($str.isNotEmpty("a "));//true
log($str.isNotEmpty("  "));//false
log($str.isNotEmpty(null));//false
```


### emptyIfNull(str)

> 当传入字符串是 null 时返回空字符串；否则原样返回。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 原字符串，或当它为 null 时返回空字符串 ""
- 版本 : 1.0.0


```javascript
log($str.emptyIfNull("  "));//"  "
log($str.emptyIfNull("嘿嘿"));//"嘿嘿"
log($str.emptyIfNull(null));//""
```


### nullToEmpty(str)

> 当传入字符串是 null 时返回空字符串；否则原样返回（作用与 emptyIfNull 相同）。
> 
> 只要不是 null，即使是纯空格也会原样返回。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 原字符串，或当它为 null 时返回空字符串 ""
- 版本 : 1.0.0


```javascript
log($str.nullToEmpty("  "));//"  "
log($str.nullToEmpty("嘿嘿"));//"嘿嘿"
log($str.nullToEmpty(null));//""
```


### nullToDefault(str, def)

> 当传入字符串是 null 时返回你给的默认值 def；否则原样返回。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : def {string} 当入参为 null/空时，要返回的默认字符串
- 返回 : {string} 原字符串，或当它为 null 时返回默认值 def
- 版本 : 1.0.0


```javascript
log($str.nullToDefault("  ","默认")); //"  "
log($str.nullToDefault("嘿嘿","默认")); //"嘿嘿"
log($str.nullToDefault(null,"默认")); //"默认"
```


### emptyToDefault(str, def)

> 空串转默认字符串
> 
> 纯空格、null、空串都会被当成空，从而返回默认值。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : def {string} 当入参为 null/空时，要返回的默认字符串
- 返回 : {string} 原字符串，或当它为 null/空/纯空格时返回默认值 def
- 版本 : 1.0.0


```javascript
log($str.emptyToDefault("  ","默认")); //"默认"
log($str.emptyToDefault("嘿嘿","默认")); //"嘿嘿"
log($str.emptyToDefault(null,"默认")); //"默认"
```


### subStart(input, length)

> 截取开头字符

- 参数 : input {string} 要处理的原始字符串
- 参数 : length {int} 要截取/补齐到的字符个数
- 返回 : {string} 从开头截取指定长度后的新字符串；长度超过原串时返回原串
- 版本 : 1.0.0


```javascript
log($str.subStart("ABCDEFG",100)); //"ABCDEFG"
log($str.subStart("ABCDEFG",7)); //"ABCDEFG"
log($str.subStart("ABCDEFG",3)); //"ABC"
```


### subEnd(input, length)

> 截取末尾字符

- 参数 : input {string} 要处理的原始字符串
- 参数 : length {int} 要截取/补齐到的字符个数
- 返回 : {string} 从末尾截取指定长度后的新字符串；长度超过原串时返回原串
- 版本 : 1.0.0


```javascript
log($str.subEnd("ABCDEFG",100)); //"ABCDEFG"
log($str.subEnd("ABCDEFG",7)); //"ABCDEFG"
log($str.subEnd("ABCDEFG",3)); //"EFG"
log($str.subEnd("ABCDEFG",2)); //"FG"
log($str.subEnd("ABCDEFG",1)); //"G"
```


### trim(str)

> 去除首尾空格
> 
> 入参为 null 时按空串处理，返回空字符串 ""。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 去掉两端空格后的新字符串；null 按空串处理
- 版本 : 1.0.0


```javascript
log($str.trim(" ABCDEFG ")); //"ABCDEFG"
```


### trimStart(str)

> 去除开头空格
> 
> 只去掉开头的空格，结尾空格保留；null 返回空串。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 只去掉开头空格后的新字符串；null 按空串处理
- 版本 : 1.0.0


```javascript
log($str.trimStart(" ABCDEFG ")); //"ABCDEFG "
log($str.trimStart(null)); //""
```


### trimEnd(str)

> 去除结尾空格
> 
> 只去掉结尾的空格，开头空格保留；null 返回空串。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 只去掉结尾空格后的新字符串；null 按空串处理
- 版本 : 1.0.0


```javascript
log($str.trimEnd(" ABCDEFG ")); //" ABCDEFG"
log($str.trimEnd(null)); //""
```


### trim(str, mode)

> 根据模式去除空格

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : mode {int} 处理模式编号：0=去掉首尾空格，1=只去掉开头，2=只去掉结尾，其它值不处理
- 返回 : {string} 去掉两端空格后的新字符串；null 按空串处理
- 版本 : 1.0.0


```javascript
log($str.trim(" ABCDEFG ",0)); //"ABCDEFG"(去除首尾)
log($str.trim(" ABCDEFG ",1)); //"ABCDEFG "(去除开头)
log($str.trim(" ABCDEFG ",2)); //" ABCDEFG"(去除结尾)
log($str.trim(" ABCDEFG ",100)); //" ABCDEFG "(啥也不干)
log($str.trim(null,0)); //""
log($str.trim(null,1)); //""
log($str.trim(null,2)); //""
```


### startWith(str, prefix, ignoreCase)

> 是否以前缀开头

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {boolean} true 表示以指定前缀开头，false 表示不是
- 版本 : 1.0.0


```javascript
var result = $str.startWith("sample", "_", true);
```


### startWith(str, prefix)

> 是否以前缀开头
> 
> 这个版本默认区分英文大小写。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 返回 : {boolean} true 表示以指定前缀开头，false 表示不是
- 版本 : 1.0.0


```javascript
var result = $str.startWith("sample", "_");
```


### startWithIgnoreEquals(str, prefix)

> 判断字符序列是否以指定前缀开头，忽略相等比较（暂未明确相等比较的具体含义，这里忽略此含义）

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 返回 : {boolean} true 表示以指定前缀开头（忽略完全相等的特殊处理）
- 版本 : 1.0.0


```javascript
var result = $str.startWithIgnoreEquals("sample", "_");
```


### startWithIgnoreCase(str, prefix)

> 判断字符序列是否以指定前缀开头，忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 返回 : {boolean} true 表示以指定前缀开头（不区分大小写）
- 版本 : 1.0.0


```javascript
var result = $str.startWithIgnoreCase("sample", "_");
```


### startWithAny(str, prefixes)

> 判断字符序列是否以指定前缀数组中的任意一个前缀开头

- 参数 : str {String} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefixes {string[]} 候选前缀字符串列表，只要命中其中任意一个即算通过
- 返回 : {boolean} 列表里任意一个前缀匹配即返回 true
- 版本 : 1.0.0


```javascript
var result = $str.startWithAny("sample", ["alpha", "beta"]);
```


### startWithAnyIgnoreCase(str, prefixes)

> 判断字符序列是否以指定前缀数组中的任意一个前缀开头，忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefixes {string[]} 候选前缀字符串列表，只要命中其中任意一个即算通过
- 返回 : {boolean} 列表里任意一个前缀匹配（忽略大小写）即返回 true
- 版本 : 1.0.0


```javascript
var result = $str.startWithAnyIgnoreCase("sample", ["alpha", "beta"]);
```


### endWith(str, suffix, ignoreCase)

> 判断字符串是否以指定后缀结尾，可选择是否忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {boolean} true 表示以指定后缀结尾，false 表示不是
- 版本 : 1.0.0


```javascript
var result = $str.endWith("sample", "_", true);
```


### endWith(str, suffix, ignoreCase, ignoreEquals)

> 判断字符串是否以指定后缀结尾，可选择是否忽略大小写和是否忽略相等

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 参数 : ignoreEquals {boolean} 为 true 时只要后缀匹配即返回；为 false 时还要额外排除“字符串本身就等于后缀”的情况
- 返回 : {boolean} true 表示以指定后缀结尾，false 表示不是
- 版本 : 1.0.0


```javascript
var result = $str.endWith("sample", "_", true, true);
```


### endWith(str, suffix)

> 判断字符串是否以指定后缀结尾

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {boolean} true 表示以指定后缀结尾，false 表示不是
- 版本 : 1.0.0


```javascript
var result = $str.endWith("sample", "_");
```


### endWithIgnoreCase(str, suffix)

> 判断字符串是否以指定后缀结尾，忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {boolean} true 表示以指定后缀结尾（不区分大小写）
- 版本 : 1.0.0


```javascript
var result = $str.endWithIgnoreCase("sample", "_");
```


### endWithAny(str, suffixes)

> 判断字符串是否以指定后缀中的任意一个结尾

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffixes {string[]} 候选后缀字符串列表，只要命中其中任意一个即算通过
- 返回 : {boolean} 列表里任意一个后缀匹配即返回 true
- 版本 : 1.0.0


```javascript
var result = $str.endWithAny("sample", ["alpha", "beta"]);
```


### endWithAnyIgnoreCase(str, suffixes)

> 判断字符串是否以指定后缀中的任意一个结尾，忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffixes {string[]} 候选后缀字符串列表，只要命中其中任意一个即算通过
- 返回 : {boolean} 列表里任意一个后缀匹配（忽略大小写）即返回 true
- 版本 : 1.0.0


```javascript
var result = $str.endWithAnyIgnoreCase("sample", ["alpha", "beta"]);
```


### contains(str, searchStr)

> 判断字符串是否包含指定子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 返回 : {boolean} true 表示原字符串包含该子串，false 表示不包含
- 版本 : 1.0.0


```javascript
var result = $str.contains("sample", "a");
```


### has(str, searchStr)

> 判断字符串是否包含指定子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 返回 : {boolean} true 表示原字符串包含该子串，false 表示不包含
- 版本 : 1.0.0


```javascript
var result = $str.has("sample", "a");
```


### containsAny(str, sreArr)

> 判断字符串是否包含指定子字符串数组中的任意一个

- 参数 : str {str} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : sreArr {string[]} 待匹配的候选子串列表，命中任意一个即算通过
- 返回 : {boolean} 列表里任意一个子串被包含即返回 true
- 版本 : 1.0.0


```javascript
var strArr = ["main","splash","welcome","start"];
var hasStr = $str.containsAny("ada main asd",strArr);
if (hasStr) {
    alert("判断字符串","包含");
} else {
    alert("判断字符串","不包含");
}
```


### containsAll(str, testChars)

> 判断字符串是否包含指定字符数组中的所有字符

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : testChars {string[]} 待匹配的候选子串列表，要求全部都包含才算通过
- 返回 : {boolean} 列表里所有子串都被包含才返回 true，否则 false
- 版本 : 1.0.0


```javascript
var result = $str.containsAll("sample", ["alpha", "beta"]);
```


### containsBlank(str)

> 判断字符串是否包含空白字符

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {boolean} true 表示原字符串里含有空格/Tab 等空白字符
- 版本 : 1.0.0


```javascript
var result = $str.containsBlank("sample");
```


### getContainsStr(str, testStrs)

> 获取字符串中包含的指定子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : testStrs {string[]} 待匹配的候选子串列表，命中任意一个即算通过
- 返回 : {string} 原字符串里实际命中的那个子串；一个都没命中返回 null
- 版本 : 1.0.0


```javascript
var result = $str.getContainsStr("sample", ["alpha", "beta"]);
```


### containsIgnoreCase(str, testStr)

> 判断字符串是否包含指定子字符串，忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : testStr {string} 要在原字符串里查找的子串
- 返回 : {boolean} true 表示包含该子串（不区分大小写）
- 版本 : 1.0.0


```javascript
var result = $str.containsIgnoreCase("sample", "sample");
```


### containsAnyIgnoreCase(str, testStrs)

> 判断字符串是否包含指定子字符串数组中的任意一个，忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : testStrs {string[]} 待匹配的候选子串列表，命中任意一个即算通过
- 返回 : {boolean} 列表里任意一个子串被包含（忽略大小写）即返回 true
- 版本 : 1.0.0


```javascript
var result = $str.containsAnyIgnoreCase("sample", ["alpha", "beta"]);
```


### getContainsStrIgnoreCase(str, testStrs)

> 获取字符串中包含的指定子字符串，忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : testStrs {string[]} 待匹配的候选子串列表，命中任意一个即算通过
- 返回 : {string} 忽略大小写后实际命中的那个子串；没命中返回 null
- 版本 : 1.0.0


```javascript
var result = $str.getContainsStrIgnoreCase("sample", ["alpha", "beta"]);
```


### indexOfIgnoreCase(str, searchStr)

> 获取指定子字符串在字符串中第一次出现的索引，忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 返回 : {int} 子串第一次出现的下标（从 0 开始），找不到返回 -1
- 版本 : 1.0.0


```javascript
var result = $str.indexOfIgnoreCase("sample", "a");
```


### indexOfIgnoreCase(str, searchStr, fromIndex)

> 获取指定子字符串在字符串中从指定位置开始第一次出现的索引，忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : fromIndex {int} 从第几个字符开始查找，下标从 0 开始
- 返回 : {int} 子串第一次出现的下标（从 0 开始），找不到返回 -1
- 版本 : 1.0.0


```javascript
var result = $str.indexOfIgnoreCase("sample", "a", 0);
```


### indexOf(text, searchStr, from, ignoreCase)

> 获取指定子字符串在字符串中从指定位置开始第一次出现的索引，可选择是否忽略大小写

- 参数 : text {string} 被搜索的原字符串
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : from {int} 从第几个字符开始查找，下标从 0 开始
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {int} 子串出现的下标（从 0 开始），找不到返回 -1
- 版本 : 1.0.0


```javascript
var result = $str.indexOf("sample", "a", 0, true);
```


### lastIndexOfIgnoreCase(str, searchStr)

> 获取指定子字符串在字符串中最后一次出现的索引，忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 返回 : {int} 子串最后一次出现的下标（从 0 开始），找不到返回 -1
- 版本 : 1.0.0


```javascript
var result = $str.lastIndexOfIgnoreCase("sample", "a");
```


### lastIndexOfIgnoreCase(str, searchStr, fromIndex)

> 获取指定子字符串在字符串中从指定位置开始最后一次出现的索引，忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : fromIndex {int} 从第几个字符开始查找，下标从 0 开始
- 返回 : {int} 子串最后一次出现的下标（从 0 开始），找不到返回 -1
- 版本 : 1.0.0


```javascript
var result = $str.lastIndexOfIgnoreCase("sample", "a", 0);
```


### cleanBlank(str)

> 清除字符串中的空白字符

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 去掉所有空白字符后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.cleanBlank("sample");
```


### stripIgnoreCase(str, prefixOrSuffix)

> 忽略大小写地去除字符串的前缀或后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefixOrSuffix {string} 要去掉的前缀或后缀（前后任意一端匹配就去掉）
- 返回 : {string} 去掉开头/结尾匹配到的前缀或后缀（忽略大小写）后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.stripIgnoreCase("sample", "_");
```


### stripIgnoreCase(str, prefix, suffix)

> 忽略大小写地去除字符串的前缀和后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 去掉开头/结尾匹配到的前缀或后缀（忽略大小写）后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.stripIgnoreCase("sample", "_", "_");
```


### strip(str, prefixOrSuffix)

> 去除字符串的前缀或后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefixOrSuffix {string} 要去掉的前缀或后缀（前后任意一端匹配就去掉）
- 返回 : {string} 去掉开头前缀、结尾后缀后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.strip("sample", "_");
```


### strip(str, prefix, suffix)

> 去除字符串的前缀和后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 去掉开头前缀、结尾后缀后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.strip("sample", "_", "_");
```


### strip(str, prefix, suffix, ignoreCase)

> 去除字符串的前缀和后缀，可选择是否忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {string} 去掉开头前缀、结尾后缀后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.strip("sample", "_", "_", true);
```


### stripAll(str, prefixOrSuffix)

> 去除字符串中所有的前缀或后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefixOrSuffix {string} 要去掉的前缀或后缀（前后任意一端匹配就去掉）
- 返回 : {string} 反复去掉开头前缀、结尾后缀后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.stripAll("sample", "_");
```


### stripAll(str, prefix, suffix)

> 去除字符串中所有的前缀和后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 反复去掉开头前缀、结尾后缀后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.stripAll("sample", "_", "_");
```


### addPrefixIfNot(str, prefix)

> 如果字符串没有指定前缀，则添加该前缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 返回 : {string} 如果原串还没有该前缀就补上，返回处理后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.addPrefixIfNot("sample", "_");
```


### addSuffixIfNot(str, suffix)

> 如果字符串没有指定后缀，则添加该后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 如果原串还没有该后缀就补上，返回处理后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.addSuffixIfNot("sample", "_");
```


### splitToLong(str, separator)

> 把字符串按分隔符切成多段，再把每段解析成整数，组成 long 数组返回。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : separator {string} 分隔符，按它把原字符串切成多段
- 返回 : {string[]} 切分并转换得到的 long 数组，转换失败的元素为 0
- 版本 : 1.0.0


```javascript
var result = $str.splitToLong("sample", ",");
```


### splitToInt(str, separator)

> 把字符串按分隔符切成多段，再把每段解析成整数，组成 int 数组返回。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : separator {string} 分隔符，按它把原字符串切成多段
- 返回 : {string[]} 切分并转换得到的 int 数组，转换失败的元素为 0
- 版本 : 1.0.0


```javascript
var result = $str.splitToInt("sample", ",");
```


### splitToArray(str, separator)

> 将字符串按指定字符序列分隔成字符串数组

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : separator {string} 分隔符，按它把原字符串切成多段
- 返回 : {string[]} 切分得到的字符串数组
- 版本 : 1.0.0


```javascript
var result = $str.splitToArray("sample", ",");
```


### splitTrim(str, regex)

> 分割并且去除首尾空格

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : regex {string} 用作分隔符的正则表达式
- 返回 : {string[]} 切分并清洗后得到的字符串列表
- 版本 : 1.0.0


```javascript
var result = $str.splitTrim("sample", "[a-z]+");
```


### splitTrim(str, separator, limit)

> 将字符串按指定字符序列分隔成字符串列表，限制列表长度，并去除每个元素的前后空白字符

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : separator {string} 分隔符，按它把原字符串切成多段
- 参数 : limit {int} 最多切成几份，<=0 表示不限制
- 返回 : {string[]} 切分并清洗后得到的字符串列表
- 版本 : 1.0.0


```javascript
var result = $str.splitTrim("sample", ",", 8);
```


### toUnderlineCase(str)

> 将输入的字符序列转换为下划线格式的字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 转成下划线命名后的字符串，如 UserName -> user_name
- 版本 : 1.0.0


```javascript
var result = $str.toUnderlineCase("sample");
```


### toCamelCase(name)

> 将输入的字符序列转换为驼峰格式的字符串

- 参数 : name {string} 要转成驼峰命名的名字，如 "user_name"
- 返回 : {string} 转成小驼峰命名后的字符串，如 user_name -> userName
- 版本 : 1.0.0


```javascript
var result = $str.toCamelCase("sample");
```


### isSurround(str, prefix, suffix)

> 判断输入的字符序列是否以指定的前缀和后缀包围

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {boolean} true 表示字符串同时以指定前缀开头、以指定后缀结尾
- 版本 : 1.0.0


```javascript
var result = $str.isSurround("sample", "_", "_");
```


### builder(strs)

> 用一个字符串列表，创建一个字符串构建器 StringBuilder，方便继续高效拼接。

- 参数 : strs {string[]} 字符串列表
- 返回 : {StringBuilder} 新建的 StringBuilder 对象，可继续 append 拼接
- 版本 : 1.0.0


```javascript
var result = $str.builder(["alpha", "beta"]);
```


### concat(isNullToEmpty, strs)

> 把列表里的多段字符串拼成一个完整字符串。

- 参数 : isNullToEmpty {boolean} 列表中的 null 是否当作空字符串参与拼接
- 参数 : strs {string[]} 字符串列表
- 返回 : {string} 列表拼接后的字符串
- 版本 : 1.0.0


```javascript
var result = $str.concat(true, ["alpha", "beta"]);
```


### brief(str, maxLength)

> 截取输入的字符序列，使其长度不超过指定的最大长度

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : maxLength {int} 结果最长保留多少个字符，超出的部分会被截掉
- 返回 : {string} 超长时被截断并加上省略号后的简短字符串
- 版本 : 1.0.0


```javascript
var result = $str.brief("sample", 8);
```


### join(conjunction, objs)

> 使用指定的连接词连接输入的对象数组

- 参数 : conjunction {string} 把多段内容拼起来时中间插入的连接符，如 ","
- 参数 : objs {Object...} 要连接起来的若干个对象，会逐个转成字符串
- 返回 : {string} 用连接符把所有对象连接成的一个字符串
- 版本 : 1.0.0


```javascript
var result = $str.join(",", "a", "b");
```


### isNumeric(str)

> 判断输入的字符序列是否为数字

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {boolean} true 表示整个字符串都是数字
- 版本 : 1.0.0


```javascript
var result = $str.isNumeric("sample");
```


### move(str, startInclude, endExclude, moveLength)

> 将输入的字符序列的指定子串移动指定的长度

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : startInclude {int} 区间起点下标（包含该位置）
- 参数 : endExclude {int} 区间终点下标（不包含该位置）
- 参数 : moveLength {int} 要把这段字符往后移动多少位
- 返回 : {string} 把指定区间的一段字符移动位置后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.move("sample", 0, 2, 8);
```


### isCharEquals(str)

> 判断输入的字符序列是否所有字符都相等

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {boolean} true 表示字符串里所有字符都相同
- 版本 : 1.0.0


```javascript
var result = $str.isCharEquals("sample");
```


### normalize(str)

> 对输入的字符序列进行规范化处理，去除首尾空格

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 规范化（折叠空白等）后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.normalize("sample");
```


### hasLetter(str)

> 判断输入的字符序列是否包含字母

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {boolean} true 表示字符串里含有英文字母
- 版本 : 1.0.0


```javascript
var result = $str.hasLetter("sample");
```


### commonPrefix(str1, str2)

> 找出两个字符序列的公共前缀

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : str2 {string} 参与比较的第二个字符串
- 返回 : {string} 两个字符串从开头算起的最长公共前缀
- 版本 : 1.0.0


```javascript
var result = $str.commonPrefix("alpha", "alpha");
```


### commonSuffix(str1, str2)

> 找出两个字符序列的公共后缀

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : str2 {string} 参与比较的第二个字符串
- 返回 : {string} 两个字符串从末尾算起的最长公共后缀
- 版本 : 1.0.0


```javascript
var result = $str.commonSuffix("alpha", "alpha");
```


### isBlankIfStr(obj)

> 判断输入的对象如果是字符串则是否为空白字符串

- 参数 : obj {object} 任意对象，方法内部会把它转成字符串
- 返回 : {boolean} 若 obj 是字符串则按空白判断，其它类型一律返回 false
- 版本 : 1.0.0


```javascript
var result = $str.isBlankIfStr(42);
```


### isEmptyIfStr(obj)

> 判断输入的对象如果是字符串则是否为空字符串

- 参数 : obj {object} 任意对象，方法内部会把它转成字符串
- 返回 : {boolean} 若 obj 是字符串则按空判断，其它类型一律返回 false
- 版本 : 1.0.0


```javascript
var result = $str.isEmptyIfStr(42);
```


### trim(strs)

> 去除字符串数组中每个字符串的首尾空格

- 参数 : strs {string[]} 字符串列表
- 版本 : 1.0.0


```javascript
$str.trim(["alpha", "beta"]);
```


### utf8Str(obj)

> 把任意对象（常见是字节数组）按 UTF-8 编码还原成字符串。

- 参数 : obj {object} 任意对象，方法内部会把它转成字符串
- 返回 : {string} 对象按 UTF-8 转成的字符串
- 版本 : 1.0.0


```javascript
var result = $str.utf8Str(42);
```


### str(obj, charsetName)

> 将输入的对象转换为指定字符集编码的字符串

- 参数 : obj {object} 任意对象，方法内部会把它转成字符串
- 参数 : charsetName {string} 字符编码名称，如 "UTF-8"、"GBK"；传 null 用默认编码
- 返回 : {string} 转成的字符串；字节数组按指定编码还原
- 版本 : 1.0.0


```javascript
var result = $str.str(42, "UTF-8");
```


### str(bytes, charset)

> 将输入的字节数组转换为指定字符集编码的字符串

- 参数 : bytes {byte[]} 字节数组，要按指定编码还原成文字
- 参数 : charset {string} 字符编码名称，如 "UTF-8"、"GBK"
- 返回 : {string} 转成的字符串；字节数组按指定编码还原
- 版本 : 1.0.0


```javascript
var result = $str.str([65, 66], "UTF-8");
```


### repeat(str, count)

> 将指定字符序列重复指定次数并返回结果字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : count {int} 重复次数，传 0 或负数返回空串
- 返回 : {string} 把原字符串重复 count 次后拼成的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.repeat("sample", 8);
```


### repeatByLength(str, padLen)

> 将指定字符序列重复直到达到指定长度并返回结果字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : padLen {int} 要补齐到的总长度
- 返回 : {string} 按指定总长度重复补齐后的字符串
- 版本 : 1.0.0


```javascript
var result = $str.repeatByLength("sample", 8);
```


### repeatAndJoin(str, count, delimiter)

> 将指定字符序列重复指定次数，并使用指定分隔符连接，返回结果字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : count {int} 重复次数，传 0 或负数返回空串
- 参数 : delimiter {string} 重复拼接时每两段之间插入的分隔符
- 返回 : {string} 重复 count 次、每两段之间用分隔符连接后的字符串
- 版本 : 1.0.0


```javascript
var result = $str.repeatAndJoin("sample", 8, "sample");
```


### equals(str1, str2)

> 比较两个字符序列是否相等

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : str2 {string} 参与比较的第二个字符串
- 返回 : {boolean} true 表示两个字符串内容相等
- 版本 : 1.0.0


```javascript
var result = $str.equals("alpha", "alpha");
```


### equalsIgnoreCase(str1, str2)

> 比较两个字符序列是否相等，忽略大小写

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : str2 {string} 参与比较的第二个字符串
- 返回 : {boolean} true 表示两个字符串内容相等（不区分大小写）
- 版本 : 1.0.0


```javascript
var result = $str.equalsIgnoreCase("alpha", "alpha");
```


### equals(str1, str2, ignoreCase)

> 比较两个字符序列是否相等，可选择是否忽略大小写

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : str2 {string} 参与比较的第二个字符串
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {boolean} true 表示两个字符串内容相等
- 版本 : 1.0.0


```javascript
var result = $str.equals("alpha", "alpha", true);
```


### equalsAnyIgnoreCase(str1, strs)

> 检查一个字符序列是否与给定的多个字符序列中的任何一个相等，忽略大小写

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : strs {string[]} 字符串列表
- 返回 : {boolean} true 表示成立，false 表示不成立
- 版本 : 1.0.0


```javascript
var result = $str.equalsAnyIgnoreCase("alpha", ["alpha", "beta"]);
```


### equalsAny(str1, strs)

> 检查一个字符序列是否与给定的多个字符序列中的任何一个相等

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : strs {string[]} 字符串列表
- 返回 : {boolean} str1 与列表中任意一个相等即返回 true
- 版本 : 1.0.0


```javascript
var result = $str.equalsAny("alpha", ["alpha", "beta"]);
```


### equalsAny(str1, ignoreCase, strs)

> 检查一个字符序列是否与给定的多个字符序列中的任何一个相等，可选择是否忽略大小写

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 参数 : strs {string[]} 字符串列表
- 返回 : {boolean} str1 与列表中任意一个相等即返回 true
- 版本 : 1.0.0


```javascript
var result = $str.equalsAny("alpha", true, ["alpha", "beta"]);
```


### isSubEquals(str1, start1, str2, ignoreCase)

> 检查一个字符序列的子序列是否与另一个字符序列相等，可选择是否忽略大小写

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : start1 {int} 第一个字符串开始比较的下标位置
- 参数 : str2 {string} 参与比较的第二个字符串
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {boolean} 比较两个字符串的片段是否相同
- 版本 : 1.0.0


```javascript
var result = $str.isSubEquals("alpha", 0, "alpha", true);
```


### isSubEquals(str1, start1, str2, start2, length, ignoreCase)

> 检查一个字符序列的指定子序列是否与另一个字符序列的指定子序列相等，可选择是否忽略大小写

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : start1 {int} 第一个字符串开始比较的下标位置
- 参数 : str2 {string} 参与比较的第二个字符串
- 参数 : start2 {int} 第二个字符串开始比较的下标位置
- 参数 : length {int} 要截取/补齐到的字符个数
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {boolean} 比较两个字符串的片段是否相同
- 版本 : 1.0.0


```javascript
var result = $str.isSubEquals("alpha", 0, "alpha", 0, 8, true);
```


### format(template, params)

> 使用指定的参数格式化字符序列模板

- 参数 : template {string} 带占位符的模板字符串，占位符用 %s
- 参数 : params {Object...} 依次填入模板 %s 占位符的参数列表
- 返回 : {string} 按模板格式化好的字符串
- 版本 : 1.0.0


```javascript
var result = $str.format("Hello, %s", "a", "b");
```


### indexedFormat(pattern, arguments)

> 使用指定的参数格式化带索引的字符序列模板

- 参数 : pattern {string} 带占位符的模板字符串，占位符用 {0} {1} ……
- 参数 : arguments {Object...} 依次填入模板 {0} {1} 占位符的参数列表
- 返回 : {string} 按 {0}{1} 占位符格式化好的字符串
- 版本 : 1.0.0


```javascript
var result = $str.indexedFormat("[a-z]+", "a", "b");
```


### utf8Bytes(str)

> 把字符串按 UTF-8 编码成字节数组。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {byte[]} 字符串按 UTF-8 编码得到的字节数组
- 版本 : 1.0.0


```javascript
var result = $str.utf8Bytes("sample");
```


### bytes(str)

> 将字符序列转换为默认字符集的字节数组

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {byte[]} 字符串按指定编码得到的字节数组
- 版本 : 1.0.0


```javascript
var result = $str.bytes("sample");
```


### bytes(str, charset)

> 将字符序列转换为指定字符集的字节数组

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : charset {string} 字符编码名称，如 "UTF-8"、"GBK"
- 返回 : {byte[]} 字符串按指定编码得到的字节数组
- 版本 : 1.0.0


```javascript
var result = $str.bytes("sample", "UTF-8");
```


### wrap(str, prefixAndSuffix)

> 用指定的前缀和后缀包装字符序列

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefixAndSuffix {string} 同时当作前缀和后缀的字符串
- 返回 : {string} 被前后包裹符包起来的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.wrap("sample", "_");
```


### wrap(str, prefix, suffix)

> 用指定的前缀和后缀包装字符序列

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 被前后包裹符包起来的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.wrap("sample", "_", "_");
```


### wrapAllWithPair(prefixAndSuffix, strs)

> 用指定的前缀和后缀包装多个字符序列

- 参数 : prefixAndSuffix {string} 同时当作前缀和后缀的字符串
- 参数 : strs {string[]} 字符串列表
- 返回 : {string[]} 批量包裹后得到的字符串数组
- 版本 : 1.0.0


```javascript
var result = $str.wrapAllWithPair("_", ["alpha", "beta"]);
```


### wrapAll(prefix, suffix, strs)

> 用指定的前缀和后缀包装多个字符序列

- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 参数 : strs {string[]} 字符串列表
- 返回 : {string[]} 批量包裹后得到的字符串数组
- 版本 : 1.0.0


```javascript
var result = $str.wrapAll("_", "_", ["alpha", "beta"]);
```


### wrapIfMissing(str, prefix, suffix)

> 如果字符序列没有指定的前缀和后缀，则用其包装

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 缺前缀/后缀时才补上，返回包裹后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.wrapIfMissing("sample", "_", "_");
```


### wrapAllWithPairIfMissing(prefixAndSuffix, strs)

> 如果多个字符序列没有指定的前缀和后缀，则用其包装

- 参数 : prefixAndSuffix {string} 同时当作前缀和后缀的字符串
- 参数 : strs {string[]} 字符串列表
- 返回 : {string[]} 批量“缺了才包裹”后的字符串数组
- 版本 : 1.0.0


```javascript
var result = $str.wrapAllWithPairIfMissing("_", ["alpha", "beta"]);
```


### count(content, strForSearch)

> 统计子串在原字符串中一共出现了几次。

- 参数 : content {string} 被搜索的原字符串
- 参数 : strForSearch {string} 要统计出现次数的子串
- 返回 : {int} 子串在原字符串中出现的次数
- 版本 : 1.0.0


```javascript
var result = $str.count("sample", "a");
```


### compare(str1, str2, nullIsLess)

> 按字典顺序比较两个字符串的大小，常用于排序。

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : str2 {string} 参与比较的第二个字符串
- 参数 : nullIsLess {boolean} 遇到 null 时是否把它当作更小的值（true=null 更小，false=null 更大）
- 返回 : {int} 比较结果：负数表示 str1 小于 str2，0 表示相等，正数表示 str1 更大
- 版本 : 1.0.0


```javascript
var result = $str.compare("alpha", "alpha", true);
```


### compareIgnoreCase(str1, str2, nullIsLess)

> 按字典顺序比较两个字符串的大小（忽略英文大小写）。

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : str2 {string} 参与比较的第二个字符串
- 参数 : nullIsLess {boolean} 遇到 null 时是否把它当作更小的值（true=null 更小，false=null 更大）
- 返回 : {int} 忽略大小写的比较结果：负数/0/正数
- 版本 : 1.0.0


```javascript
var result = $str.compareIgnoreCase("alpha", "alpha", true);
```


### compareVersion(version1, version2)

> 比较两个版本号的大小

- 参数 : version1 {string} 第一个版本号字符串，如 "1.2.10"
- 参数 : version2 {string} 第二个版本号字符串，如 "1.3.0"
- 返回 : {int} 版本比较结果：负数表示 version1 更旧，0 相同，正数表示更新
- 版本 : 1.0.0


```javascript
var result = $str.compareVersion("1.2.0", "1.2.0");
```


### appendIfMissing(str, suffix, suffixes)

> 如果字符串不以指定后缀结尾，则添加后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 参数 : suffixes {string[]} 候选后缀字符串列表，只要命中其中任意一个即算通过
- 返回 : {string} 末尾缺这些后缀时补上指定后缀后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.appendIfMissing("sample", "_", ["alpha", "beta"]);
```


### appendIfMissingIgnoreCase(str, suffix, suffixes)

> 如果字符串不以指定后缀结尾（忽略大小写），则添加后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 参数 : suffixes {string[]} 候选后缀字符串列表，只要命中其中任意一个即算通过
- 返回 : {string} 处理后的新字符串（原字符串不会被改动）
- 版本 : 1.0.0


```javascript
var result = $str.appendIfMissingIgnoreCase("sample", "_", ["alpha", "beta"]);
```


### appendIfMissing(str, suffix, ignoreCase, testSuffixes)

> 如果字符串不以指定后缀结尾（可指定是否忽略大小写），则添加后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 参数 : testSuffixes {string[]} 该参数的含义见方法说明
- 返回 : {string} 末尾缺这些后缀时补上指定后缀后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.appendIfMissing("sample", "_", true, ["alpha", "beta"]);
```


### prependIfMissing(str, prefix, prefixes)

> 如果字符串不以指定前缀开头，则添加前缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : prefixes {string[]} 候选前缀字符串列表，只要命中其中任意一个即算通过
- 返回 : {string} 开头缺这些前缀时补上指定前缀后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.prependIfMissing("sample", "_", ["alpha", "beta"]);
```


### prependIfMissingIgnoreCase(str, prefix, prefixes)

> 如果字符串不以指定前缀开头（忽略大小写），则添加前缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : prefixes {string[]} 候选前缀字符串列表，只要命中其中任意一个即算通过
- 返回 : {string} 处理后的新字符串（原字符串不会被改动）
- 版本 : 1.0.0


```javascript
var result = $str.prependIfMissingIgnoreCase("sample", "_", ["alpha", "beta"]);
```


### prependIfMissing(str, prefix, ignoreCase, prefixes)

> 如果字符串不以指定前缀开头（可指定是否忽略大小写），则添加前缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 参数 : prefixes {string[]} 候选前缀字符串列表，只要命中其中任意一个即算通过
- 返回 : {string} 开头缺这些前缀时补上指定前缀后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.prependIfMissing("sample", "_", true, ["alpha", "beta"]);
```


### replaceIgnoreCase(str, searchStr, replacement)

> 忽略大小写替换字符串中的指定内容

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : replacement {string} 用来替换上去的新内容
- 返回 : {string} 替换后的新字符串（忽略大小写）
- 版本 : 1.0.0


```javascript
var result = $str.replaceIgnoreCase("sample", "a", "a");
```


### replace(str, searchStr, replacement)

> 替换字符串中的指定内容

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : replacement {string} 用来替换上去的新内容
- 返回 : {string} 替换后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.replace("sample", "a", "a");
```


### lastIndexOf(text, searchStr, from, ignoreCase)

> 从指定位置开始查找指定字符序列最后一次出现的位置，可选择是否忽略大小写

- 参数 : text {string} 被搜索的原字符串
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : from {int} 从第几个字符开始查找，下标从 0 开始
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {int} 子串最后一次出现的下标（从 0 开始），找不到返回 -1
- 版本 : 1.0.0


```javascript
var result = $str.lastIndexOf("sample", "a", 0, true);
```


### ordinalIndexOf(str, searchStr, ordinal)

> 查找第 ordinal 次出现的子串位置，例如 ordinal=2 表示找第二次出现的地方。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : ordinal {int} 要找第几次出现，从 1 开始（1=第一次）
- 返回 : {int} 第 ordinal 次出现的下标，找不到返回 -1
- 版本 : 1.0.0


```javascript
var result = $str.ordinalIndexOf("sample", "a", 0);
```


### removeAll(str, strToRemove)

> 从字符序列中移除所有指定的字符序列

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : strToRemove {string} 要从原字符串中删除掉的子串
- 返回 : {string} 删除掉所有目标子串后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removeAll("sample", "a");
```


### removeAny(str, strsToRemove)

> 从字符序列中移除指定的多个字符序列中的任意一个

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : strsToRemove {string[]} 要删除掉的若干子串组成的列表
- 返回 : {string} 删除掉列表中任意子串后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removeAny("sample", ["alpha", "beta"]);
```


### removeAllLineBreaks(str)

> 移除字符序列中的所有换行符

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 去掉所有换行符后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removeAllLineBreaks("sample");
```


### removePreAndLowerFirst(str, preLength)

> 去掉字符串开头指定个数的字符，再把剩下部分的首字母变小写。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : preLength {int} 要从开头去掉几个字符
- 返回 : {string} 去掉开头内容、首字母小写后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removePreAndLowerFirst("sample", 8);
```


### removePreAndLowerFirst(str, prefix)

> 移除字符序列的指定前缀并将第一个字符转换为小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 返回 : {string} 去掉开头内容、首字母小写后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removePreAndLowerFirst("sample", "_");
```


### removePrefix(str, prefix)

> 移除字符序列的指定前缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 返回 : {string} 开头匹配到前缀就去掉后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removePrefix("sample", "_");
```


### removeAllPrefix(str, prefix)

> 移除字符序列中所有的指定前缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 返回 : {string} 反复去掉开头前缀后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removeAllPrefix("sample", "_");
```


### removePrefixIgnoreCase(str, prefix)

> 忽略大小写地移除字符序列的指定前缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 返回 : {string} 去掉开头前缀（忽略大小写）后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removePrefixIgnoreCase("sample", "_");
```


### removeSuffix(str, suffix)

> 移除字符序列的指定后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 结尾匹配到后缀就去掉后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removeSuffix("sample", "_");
```


### removeAllSuffix(str, suffix)

> 移除字符序列中所有的指定后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 反复去掉结尾后缀后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removeAllSuffix("sample", "_");
```


### removeSufAndLowerFirst(str, suffix)

> 移除字符序列的指定后缀并将第一个字符转换为小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 去掉结尾后缀、首字母小写后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removeSufAndLowerFirst("sample", "_");
```


### removeSuffixIgnoreCase(str, suffix)

> 忽略大小写地移除字符序列的指定后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 去掉结尾后缀（忽略大小写）后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.removeSuffixIgnoreCase("sample", "_");
```


### wrapAllIfMissing(prefix, suffix, strs)

> 如果字符串数组中的每个字符串没有指定的前缀和后缀，则添加前缀和后缀

- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 参数 : strs {string[]} 字符串列表
- 返回 : {string[]} 批量“缺了才包裹”后的字符串数组
- 版本 : 1.0.0


```javascript
var result = $str.wrapAllIfMissing("_", "_", ["alpha", "beta"]);
```


### unWrap(str, prefix, suffix)

> 移除字符串的指定前缀和后缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 去掉前后包裹符后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.unWrap("sample", "_", "_");
```


### isWrap(str, prefix, suffix)

> 判断字符串是否以指定的前缀和后缀包裹

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {boolean} true 表示已经被指定前后包裹符包起来了
- 版本 : 1.0.0


```javascript
var result = $str.isWrap("sample", "_", "_");
```


### isWrap(str, wrapper)

> 判断字符串是否以指定的包裹字符串包裹

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : wrapper {string} 同时当作前缀和后缀的包裹符
- 返回 : {boolean} true 表示已经被指定前后包裹符包起来了
- 版本 : 1.0.0


```javascript
var result = $str.isWrap("sample", "_");
```


### padPre(str, length, padStr)

> 在字符串前面填充指定的字符串，直到达到指定的长度

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : length {int} 要截取/补齐到的字符个数
- 参数 : padStr {string} 用来补齐/填充的字符或字符串
- 返回 : {string} 在开头补齐到指定长度后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.padPre("sample", 8, "sample");
```


### padAfter(str, length, padStr)

> 在字符串后面填充指定的字符串，直到达到指定的长度

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : length {int} 要截取/补齐到的字符个数
- 参数 : padStr {string} 用来补齐/填充的字符或字符串
- 返回 : {string} 在结尾补齐到指定长度后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.padAfter("sample", 8, "sample");
```


### center(str, size)

> 将字符串居中，使用空格填充

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : size {int} 居中对齐后的总长度
- 返回 : {string} 居中对齐（两侧补齐）后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.center("sample", 8);
```


### center(str, size, padStr)

> 将字符串居中，使用指定的字符串填充

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : size {int} 居中对齐后的总长度
- 参数 : padStr {string} 用来补齐/填充的字符或字符串
- 返回 : {string} 居中对齐（两侧补齐）后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.center("sample", 8, "sample");
```


### replace(str, searchStr, replacement, ignoreCase)

> 替换字符串中所有匹配的子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : replacement {string} 用来替换上去的新内容
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {string} 替换后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.replace("sample", "a", "a", true);
```


### replace(str, fromIndex, searchStr, replacement, ignoreCase)

> 从指定索引开始替换字符串中所有匹配的子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : fromIndex {int} 从第几个字符开始查找，下标从 0 开始
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : replacement {string} 用来替换上去的新内容
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {string} 替换后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.replace("sample", 0, "a", "a", true);
```


### replace(str, startInclude, endExclude, replacedStr)

> 替换指定范围内的子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : startInclude {int} 区间起点下标（包含该位置）
- 参数 : endExclude {int} 区间终点下标（不包含该位置）
- 参数 : replacedStr {string} 用来替换上去的新内容
- 返回 : {string} 替换后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.replace("sample", 0, 2, "a");
```


### replaceLast(str, searchStr, replacedStr)

> 替换字符串中最后一个匹配的子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : replacedStr {string} 用来替换上去的新内容
- 返回 : {string} 只替换最后一次出现的子串后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.replaceLast("sample", "a", "a");
```


### replaceLast(str, searchStr, replacedStr, ignoreCase)

> 替换字符串中最后一个匹配的子字符串，可选择是否忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : replacedStr {string} 用来替换上去的新内容
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {string} 只替换最后一次出现的子串后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.replaceLast("sample", "a", "a", true);
```


### replaceFirst(str, searchStr, replacedStr)

> 替换字符串中第一个匹配的子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : replacedStr {string} 用来替换上去的新内容
- 返回 : {string} 只替换第一次出现的子串后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.replaceFirst("sample", "a", "a");
```


### replaceFirst(str, searchStr, replacedStr, ignoreCase)

> 替换字符串中第一个匹配的子字符串，可选择是否忽略大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : searchStr {string} 要在原字符串里查找的子串
- 参数 : replacedStr {string} 用来替换上去的新内容
- 参数 : ignoreCase {boolean} 是否忽略英文大小写，true 表示不区分 a 与 A
- 返回 : {string} 只替换第一次出现的子串后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.replaceFirst("sample", "a", "a", true);
```


### hide(str, startInclude, endExclude)

> 隐藏指定范围内的字符

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : startInclude {int} 区间起点下标（包含该位置）
- 参数 : endExclude {int} 区间终点下标（不包含该位置）
- 返回 : {string} 把指定区间的字符用 * 打码后的新字符串（常用于隐藏手机号中间几位）
- 版本 : 1.0.0


```javascript
var result = $str.hide("sample", 0, 2);
```


### replaceChars(str, chars, replacedStr)

> 替换字符串中指定字符集合中的字符

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : chars {string} 其中任意一个字符出现都要被替换
- 参数 : replacedStr {string} 用来替换上去的新内容
- 返回 : {string} 把字符集合中任意字符都替换后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.replaceChars("sample", "sample", "a");
```


### length(cs)

> 获取字符串的长度

- 参数 : cs {string} 要取长度的字符串
- 返回 : {int} 字符串的字符个数；null 返回 0
- 版本 : 1.0.0


```javascript
var result = $str.length("sample");
```


### totalLength(strs)

> 获取多个字符串的总长度

- 参数 : strs {string[]} 字符串列表
- 返回 : {int} 列表里所有字符串长度之和；null 按 0 算
- 版本 : 1.0.0


```javascript
var result = $str.totalLength(["alpha", "beta"]);
```


### maxLength(string, length)

> 如果字符串长度超过指定长度，截取到指定长度

- 参数 : string {string} 要处理的原始字符串
- 参数 : length {int} 要截取/补齐到的字符个数
- 返回 : {string} 超长则截断到指定长度后的字符串
- 版本 : 1.0.0


```javascript
var result = $str.maxLength("sample", 8);
```


### upperFirstAndAddPre(str, preString)

> 将字符串首字母大写并添加前缀

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : preString {string} 首字母大写后，还要额外拼在最前面的字符串
- 返回 : {string} 开头拼上前缀、再把首字母大写后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.upperFirstAndAddPre("sample", "sample");
```


### upperFirst(str)

> 将字符串首字母大写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 首字母大写、其余不变的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.upperFirst("sample");
```


### lowerFirst(str)

> 将字符串首字母小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 首字母小写、其余不变的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.lowerFirst("sample");
```


### isUpperCase(str)

> 判断字符串是否全部为大写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {boolean} true 表示整串都是大写字母
- 版本 : 1.0.0


```javascript
var result = $str.isUpperCase("sample");
```


### isLowerCase(str)

> 判断字符串是否全部为小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {boolean} true 表示整串都是小写字母
- 版本 : 1.0.0


```javascript
var result = $str.isLowerCase("sample");
```


### swapCase(str)

> 反转字符串的大小写

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 大小写互换后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.swapCase("sample");
```


### toString(obj)

> 将对象转换为字符串

- 参数 : obj {object} 任意对象，方法内部会把它转成字符串
- 返回 : {string} 对象转成的字符串；null 返回 "null"
- 版本 : 1.0.0


```javascript
var result = $str.toString(42);
```


### toStringOrNull(obj)

> 把对象转成字符串；对象为 null 时返回 null。

- 参数 : obj {object} 任意对象，方法内部会把它转成字符串
- 返回 : {string} 对象转成的字符串；对象为 null 时返回 null
- 版本 : 1.0.0


```javascript
var result = $str.toStringOrNull(42);
```


### toStringOrEmpty(obj)

> 把对象转成字符串；对象为 null 时返回空字符串。

- 参数 : obj {object} 任意对象，方法内部会把它转成字符串
- 返回 : {string} 对象转成的字符串；对象为 null 时返回空串
- 版本 : 1.0.0


```javascript
var result = $str.toStringOrEmpty(42);
```


### builder()

> 用一个字符串列表，创建一个字符串构建器 StringBuilder，方便继续高效拼接。

- 返回 : {StringBuilder} 新建的 StringBuilder 对象，可继续 append 拼接
- 版本 : 1.0.0


```javascript
var result = $str.builder();
```


### builder(capacity)

> 用一个字符串列表，创建一个字符串构建器 StringBuilder，方便继续高效拼接。

- 参数 : capacity {int} 字符串构建器的初始容量（预估要拼多长，给大一点更快）
- 返回 : {StringBuilder} 新建的 StringBuilder 对象，可继续 append 拼接
- 版本 : 1.0.0


```javascript
var result = $str.builder(8);
```


### reverse(str)

> 反转字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 返回 : {string} 倒序后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.reverse("sample");
```


### similar(str1, str2)

> 计算两个字符串的相似度，返回相似度比例（0.0 - 1.0）

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : str2 {string} 参与比较的第二个字符串
- 返回 : {double} 两个字符串的相似度（0~1 的小数，越接近 1 越像）
- 版本 : 1.0.0


```javascript
var result = $str.similar("alpha", "alpha");
```


### similar(str1, str2, scale)

> 计算两个字符串的相似度，并按 scale 指定的小数位数格式化成字符串返回。

- 参数 : str1 {string} 参与比较的第一个字符串
- 参数 : str2 {string} 参与比较的第二个字符串
- 参数 : scale {int} 相似度结果保留几位小数
- 返回 : {string} 两个字符串的相似度（0~1 的小数，越接近 1 越像）
- 版本 : 1.0.0


```javascript
var result = $str.similar("alpha", "alpha", 8);
```


### uuid()

> 生成一个随机的 UUID（一串几乎不可能重复的唯一编号）。

- 返回 : {string} 一个随机生成的 UUID 字符串
- 版本 : 1.0.0


```javascript
var result = $str.uuid();
```


### split(str, separator, limit, isTrim, ignoreEmpty)

> 按照指定分隔符分割字符串序列，可设置分割次数限制、是否去除前后空格、是否忽略空字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : separator {string} 分隔符，按它把原字符串切成多段
- 参数 : limit {int} 最多切成几份，<=0 表示不限制
- 参数 : isTrim {boolean} 拆分后是否去掉每一段两端的空格
- 参数 : ignoreEmpty {boolean} 拆分后是否丢弃空的片段
- 返回 : {string[]} 处理得到的字符串数组/列表
- 版本 : 1.0.0


```javascript
var result = $str.split("sample", ",", 8, true, true);
```


### split(str, len)

> 按照指定长度分割字符序列

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : len {int} 要截取的字节/字符长度
- 返回 : {string[]} 处理得到的字符串数组/列表
- 版本 : 1.0.0


```javascript
var result = $str.split("sample", 2);
```


### split(str, separator)

> 按指定分隔符拆分字符串，并按原顺序返回各段；末尾的空片段也会保留。
> 原字符串不会被修改，方法会返回一个新字符串；传入 null 时按各方法约定处理。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : separator {string} 分隔符，按它把原字符串切成多段
- 返回 : {string[]} 处理得到的字符串数组/列表


```javascript
var parts = $str.split("red,green,blue", ",");
```


### cut(str, partLength)

> 按照指定长度切割字符序列

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : partLength {int} 每一份切多长
- 返回 : {string[]} 按固定长度切好的字符串数组
- 版本 : 1.0.0


```javascript
var result = $str.cut("sample", 8);
```


### sub(str, fromIndexInclude, toIndexExclude)

> 截取字符序列中指定范围的子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : fromIndexInclude {int} 截取区间起点下标（包含）
- 参数 : toIndexExclude {int} 截取区间终点下标（不包含）
- 返回 : {string} 截取指定区间后的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.sub("sample", 0, 0);
```


### subPreGbk(str, len, suffix)

> 按 GBK 编码截取开头指定字节长度的前半段，保证不会把一个汉字切成一半而出现乱码。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : len {int} 要截取的字节/字符长度
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string} 按 GBK 字节截取的前半段字符串，不会截出半个汉字
- 版本 : 1.0.0


```javascript
var result = $str.subPreGbk("sample", 2, "_");
```


### subPreGbk(str, len, halfUp)

> 按 GBK 编码截取开头指定字节长度的前半段，保证不会把一个汉字切成一半而出现乱码。

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : len {int} 要截取的字节/字符长度
- 参数 : halfUp {boolean} 按 GBK 截断时，遇到半个汉字是否向上补全以避免乱码
- 返回 : {string} 按 GBK 字节截取的前半段字符串，不会截出半个汉字
- 版本 : 1.0.0


```javascript
var result = $str.subPreGbk("sample", 2, true);
```


### subPre(string, toIndexExclude)

> 截取字符序列中从开头到指定位置（不包含）的子字符串

- 参数 : string {string} 要处理的原始字符串
- 参数 : toIndexExclude {int} 截取区间终点下标（不包含）
- 返回 : {string} 从开头截取到指定下标的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.subPre("sample", 0);
```


### subSuf(string, fromIndex)

> 截取字符序列中从指定位置到结尾的子字符串

- 参数 : string {string} 要处理的原始字符串
- 参数 : fromIndex {int} 从第几个字符开始查找，下标从 0 开始
- 返回 : {string} 从指定下标截取到末尾的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.subSuf("sample", 0);
```


### subSufByLength(string, length)

> 截取字符序列中从结尾开始指定长度的子字符串

- 参数 : string {string} 要处理的原始字符串
- 参数 : length {int} 要截取/补齐到的字符个数
- 返回 : {string} 从末尾截取指定长度的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.subSufByLength("sample", 8);
```


### subWithLength(input, fromIndex, length)

> 截取字符串中从指定位置开始指定长度的子字符串

- 参数 : input {string} 要处理的原始字符串
- 参数 : fromIndex {int} 从第几个字符开始查找，下标从 0 开始
- 参数 : length {int} 要截取/补齐到的字符个数
- 返回 : {string} 从指定位置开始截取指定长度的新字符串
- 版本 : 1.0.0


```javascript
var result = $str.subWithLength("sample", 0, 8);
```


### subBefore(string, separator, isLastSeparator)

> 截取之前字符串

- 参数 : string {string} 要处理的原始字符串
- 参数 : separator {string} 分隔符，按它把原字符串切成多段
- 参数 : isLastSeparator {boolean} 是否以“最后一个”分隔符为准来切分
- 返回 : {string} 分隔符之前的那一段内容
- 版本 : 1.0.0


```javascript
var result = $str.subBefore("sample", ",", true);
```


### subAfter(string, separator, isLastSeparator)

> 截取之后字符串

- 参数 : string {string} 要处理的原始字符串
- 参数 : separator {string} 分隔符，按它把原字符串切成多段
- 参数 : isLastSeparator {boolean} 是否以“最后一个”分隔符为准来切分
- 返回 : {string} 分隔符之后的那一段内容
- 版本 : 1.0.0


```javascript
var result = $str.subAfter("sample", ",", true);
```


### subBetween(str, before, after)

> 截取字符序列中两个指定分隔符之间的子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : before {string} 截取区间前面的标记字符串
- 参数 : after {string} 截取区间后面的标记字符串
- 返回 : {string} 两个标记之间夹着的内容
- 版本 : 1.0.0


```javascript
var result = $str.subBetween("sample", "sample", "sample");
```


### subBetween(str, beforeAndAfter)

> 截取字符序列中指定分隔符之间的子字符串（前后分隔符相同）

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : beforeAndAfter {string} 前后相同的标记字符串
- 返回 : {string} 两个标记之间夹着的内容
- 版本 : 1.0.0


```javascript
var result = $str.subBetween("sample", "sample");
```


### subBetweenAll(str, prefix, suffix)

> 从给定的字符序列中提取所有位于指定前缀和后缀之间的子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefix {string} 开头要匹配或添加的前缀字符串
- 参数 : suffix {string} 结尾要匹配或添加的后缀字符串
- 返回 : {string[]} 所有成对标记之间内容组成的数组
- 版本 : 1.0.0


```javascript
var result = $str.subBetweenAll("sample", "_", "_");
```


### subBetweenAll(str, prefixAndSuffix)

> 从给定的字符序列中提取所有位于指定前缀和后缀（前缀和后缀相同）之间的子字符串

- 参数 : str {string} 要处理的原始字符串；传 null 时多数方法会按空串或 false 处理
- 参数 : prefixAndSuffix {string} 同时当作前缀和后缀的字符串
- 返回 : {string[]} 所有成对标记之间内容组成的数组
- 版本 : 1.0.0


```javascript
var result = $str.subBetweenAll("sample", "_");
```


