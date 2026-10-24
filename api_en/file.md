# $file - 文件系统

- 更新时间:2026-10-22 10:55:48

> 文件系统对象（脚本里写作 $file，中文名叫 $文件）。
> 
> 它是你操作手机里各种文件、文件夹的"工具箱"：可以读文件、写文件、创建、删除、复制、移动、
> 罗列目录里有哪些文件，还能查询手机里的图片、视频、音频媒体信息。
> 
> 新手提示：路径既可以写完整绝对路径（如 "/sdcard/Download/a.txt"），也可以写相对脚本目录的
> 相对路径（如 "./main.js"、"res"）。写入操作通常需要把文件放到外部存储（SD 卡）目录。



```javascript
// 读取一个文本文件的全部内容
var text = $file.read("/sdcard/Download/config.txt");
// 把内容写到另一个新文件里，完成一次复制
$file.write(text, "/sdcard/Download/config-copy.txt");
```




### uri(path)

> 把一个本地文件路径转换成系统可共享的 Uri（内容提供者地址）。
> 
> 有时候你想把手机里的一个本地文件发给别的 App（比如微信），别的 App 不能直接访问你的
> 私有文件路径，需要先把路径"包装"成一个 Uri 地址。本方法就是干这个用的，常用于分享文件。

- 参数 : path {String} 要转换的本地文件路径（绝对路径或相对脚本目录的路径）
- 返回 : {Uri} 包装后的 Uri 对象；转换失败时可能返回 null
- 版本 : 1.3.7


```javascript
// 把一张本地图片的路径包装成 Uri，便于分享给其它 App
var uri = $file.uri("/storage/emulated/0/Pictures/小红.png");
log(uri); // 输出类似 content:// 开头的地址
```


### open(path)

> 打开（获得）一个文件对象 File，并不会真正读写文件内容。
> 
> 它只是根据路径造一个 File 对象给你，方便你后续调用 exists、isFile 之类的判断。
> 路径若写成相对路径，会自动补全到脚本所在的外部存储目录。

- 参数 : path {string} 文件或文件夹路径（绝对路径或相对路径）
- 返回 : {File} 对应的 Java File 文件对象
- 版本 : 1.0.0


```javascript
// 根据路径得到一个 File 对象（这里指向脚本目录下的 res 文件夹）
var file = $file.open("res");
log(file.getAbsolutePath()); // 输出该路径的完整绝对路径
```


### isFile(path)

> 检查路径是否为文件。
> 
> 判断这个路径指向的到底是一个"文件"（比如 main.js）还是一个"文件夹"（比如 res）。
> 如果路径根本不存在，会直接返回 false。

- 参数 : path {string} 要判断的路径（绝对路径或相对路径）
- 返回 : {boolean} 是文件返回 true，不是文件或路径不存在返回 false
- 版本 : 1.0.0


```javascript
// 判断 res 这个路径是不是文件（它其实是文件夹，所以是 false）
log($file.isFile("res"));      // false
// 判断 main.js 是不是文件（它就是一个文件，所以是 true）
log($file.isFile("main.js"));  // true
```


### isDir(path)

> 检查路径是否为目录（文件夹）。
> 
> 判断这个路径指向的是不是一个文件夹。如果路径根本不存在，会直接返回 false。

- 参数 : path {string} 要判断的路径（绝对路径或相对路径）
- 返回 : {boolean} 是文件夹返回 true，否则返回 false
- 版本 : 1.0.0


```javascript
// res 是文件夹，返回 true
log($file.isDir("res"));      // true
// main.js 是文件不是文件夹，返回 false
log($file.isDir("main.js"));  // false
```


### isEmptyDir(path)

> 判断一个文件夹是不是空的（里面没有任何文件）。
> 
> 如果路径指向的是一个普通文件，也算作"空"（返回 true）；如果路径不存在，也返回 true。

- 参数 : path {string} 要判断的文件夹路径
- 返回 : {boolean} 文件夹为空（或本身是文件、或不存在）时返回 true
- 版本 : 1.0.0


```javascript
// res 文件夹里有东西，返回 false
log($file.isEmptyDir("res")); // false
// xml 文件夹是空的，返回 true
log($file.isEmptyDir("xml")); // true
```


### isEmpty(path)

> 判断一个文件或文件夹是不是"空的"。
> 
> 如果是文件夹，就看里面有没有内容；如果是文件，就看文件里有没有写过任何内容。
> 一句话搞定，不用再分情况。

- 参数 : path {string} 要判断的文件或文件夹路径
- 返回 : {boolean} 为空返回 true，有内容返回 false
- 版本 : 1.0.0


```javascript
// res 文件夹里有东西，不是空的
log($file.isEmpty("res"));      // false
// xml 文件夹是空的
log($file.isEmpty("xml"));      // true
// main.js 文件里有内容
log($file.isEmpty("main.js"));  // false
```


### join(parent, child)

> 把两段路径拼接成一段完整路径。
> 
> 手动拼路径时最容易漏掉或多加"/"，本方法自动帮你处理好斜杠。比如父级是 "sdcard"、
> 子级是 "Pictures"，就会得到 "sdcard/Pictures"。

- 参数 : parent {string} 前面那一段路径
- 参数 : child {string} 后面要接上去的那一段路径
- 返回 : {string} 拼接好的完整路径
- 版本 : 1.0.0


```javascript
// 把两段路径拼起来，自动补好中间的斜杠
var path = $file.join("sdcard", "Pictures");
log(path); // 输出：sdcard/Pictures
```


### join(path)

> 把很多段路径依次拼接成一条完整路径。
> 
> 当你有一大堆文件夹名字需要一层层拼起来时，用这个版本最方便：把它们放进一个数组里传进去。
> 如果数组里只有一段，就直接返回那一段；数组为空则返回 null。

- 参数 : path {string[]} 由多段路径组成的数组（列表）
- 返回 : {string} 拼接好的完整路径；数组为空时返回 null
- 版本 : 1.0.0


```javascript
// 把多段路径一次拼好
var path = $file.join(["sdcard", "Pictures", "我的项目", "res"]);
log(path); // 输出：/sdcard/Pictures/我的项目/res
```


### create(path)

> 创建一个空白文件（注意：是文件，不是文件夹）。
> 
> 如果这个路径已经存在文件，就不会重复创建，直接返回 false；创建成功返回 true。
> 它只会建出一个空文件，要写内容请再调用 write。

- 参数 : path {string} 要创建的文件路径
- 返回 : {boolean} 创建成功返回 true，文件已存在或失败返回 false
- 版本 : 1.0.0


```javascript
// 在 xml/res 目录下创建一个空的 test.js 文件
var ok = $file.create("xml/res/test.js");
log("创建结果：" + ok);
```


### mkdir(path)

> 创建一个文件夹（目录）。
> 
> 如果路径里中间的文件夹不存在，会一并把它们建出来（可一次建多层）。创建成功返回 true。
> 注意区分：create 建的是文件，mkdir 建的是文件夹。

- 参数 : path {string} 要创建的文件夹路径
- 返回 : {boolean} 创建成功返回 true，失败返回 false
- 版本 : 1.0.0


```javascript
// 在 xml 目录下创建名为 kir 的文件夹
var ok = $file.mkdir("xml/kir");
log("建文件夹结果：" + ok);
```


### exists(path)

> 检查某个路径到底存不存在（不管它是文件还是文件夹）。
> 
> 操作文件前经常先问一句"它在不在？"，避免报错。存在返回 true，不存在返回 false。

- 参数 : path {string} 要检查的路径（文件或文件夹都行）
- 返回 : {boolean} 存在返回 true，不存在返回 false
- 版本 : 1.0.0


```javascript
// 先创建一个文件
$file.create("./测试文件夹/a.js");
// 再判断它是否存在
if ($file.exists("./测试文件夹/a.js")) {
    log("路径存在");
}
```


### ensureDir(path)

> 确保一个文件所在的文件夹一定存在（不存在就自动创建）。
> 
> 写文件前最怕"上级文件夹不存在"导致写入失败。本方法会顺着路径把中间缺的文件夹都建好，
> 然后原样返回这个路径，方便你接着拿去写文件。

- 参数 : path {string} 要确保其父目录存在的文件或文件夹路径
- 返回 : {string} 原样返回这个路径
- 版本 : 1.0.0


```javascript
// 确保 "./测试文件夹/demo" 这个文件夹存在（缺的层级会自动建出来）
var p = $file.ensureDir("./测试文件夹/demo/a.js");
log(p); // 返回传入的路径
```


### read(path)

> 读取一个文本文件的全部内容，按 UTF-8 编码读成字符串。
> 
> 最常用的读文件方法：把整个文本文件一次读成一大段文字。如果文件不存在，会打印警告并返回
> 空字符串 ""，不会让脚本崩溃。

- 参数 : path {string} 要读取的文本文件路径
- 返回 : {string} 文件里的文字内容；文件不存在时返回空字符串 ""
- 版本 : 1.0.0


```javascript
// 读取 main.js 这个文本文件的全部内容
var content = $file.read("./main.js");
log(content); // 打印文件里的文字
```


### read(path, encoding)

> 用指定的编码读取文本文件内容。
> 
> 默认 read 按 UTF-8 读。如果你的文件是别的编码（比如老式的 GBK/GB2312，读出来会乱码），
> 就用这个版本，把编码名传进去。

- 参数 : path {string} 要读取的文件路径
- 参数 : encoding {string} 文件编码名，如 "utf-8"、"gbk"、"gb2312"
- 返回 : {string} 文件里的文字内容；文件不存在时返回空字符串
- 版本 : 1.0.0


```javascript
// 用 GBK 编码读取文件，避免中文乱码
var content = $file.read("./main.js", "gbk");
log(content);
```


### reads(path)

> 读取文本文件，并按"行"切成一个字符串数组。
> 
> read 会得到一整段文字；reads 则会在每个换行符处切开，每一行是数组里的一个元素，
> 方便你逐行处理。文件读出来是空的时返回空数组。

- 参数 : path {string} 要读取的文本文件路径
- 返回 : {string[]} 每一行文字组成的数组；文件为空时返回空数组
- 版本 : 1.0.0


```javascript
// 把文件按行读成数组
var list = $file.reads("./main.js");
// 逐行打印（i 从 0 开始，依次取到最后一行）
for (var i = 0; i < list.length; i++) {
    log("第" + i + "行：" + list[i]);
}
```


### readByte(path)

> 读取文件的原始二进制内容（字节数组）。
> 
> 前面的 read 是按"文字"读；readByte 是按"字节"读，适合图片、音频、未知格式的二进制文件。
> 文件不存在或读取失败时返回一个空数组。

- 参数 : path {string} 要读取的文件路径
- 返回 : {byte[]} 文件的二进制字节数组；失败时返回空数组
- 版本 : 1.0.0


```javascript
// 读取一个文件的原始字节
var data = $file.readByte("./main.js");
log("一共读到 " + data.length + " 个字节");
```


### write(content, path)

> 把一段文字内容写入文件（覆盖原内容）。
> 
> 会用 UTF-8 编码写入。如果文件已经存在，原来的内容会被整个替换掉（不是追加）。
> 如果文件夹不存在会自动处理。只适用于写到外部存储。

- 参数 : content {string} 要写入的文字内容
- 参数 : path {string} 写入的目标文件路径
- 版本 : 1.0.0


```javascript
// 把文字 "我是内容" 写入 a.js，原来的内容会被覆盖
$file.write("我是内容", "./xml/a.js");
```


### write(content, path, encoding)

> 用指定编码把文字内容写入文件（覆盖原内容）。
> 
> 和 write 一样是覆盖写入，只是多了一个参数让你指定文件编码，比如写成 GBK 方便别的老软件读取。

- 参数 : content {string} 要写入的文字内容
- 参数 : path {string} 目标文件路径
- 参数 : encoding {string} 文件编码名，如 "utf-8"、"gbk"
- 版本 : 1.0.0


```javascript
// 用 GBK 编码把内容写入 a.js
$file.write("我是内容", "./code/a.js", "GBK");
```


### writes(lines, path)

> 把一个字符串数组（每行一条）整批写入文件（覆盖原内容）。
> 
> 数组里的每一项会作为一行写进去，自动加上换行。相当于把 reads 读出来的数组原样写回去。

- 参数 : lines {string[]} 要写入的多行内容数组
- 参数 : path {string} 目标文件路径
- 版本 : 1.0.0


```javascript
// 准备三行内容
var lines = ["我是内容1", "我是内容2", "我是内容3"];
// 一次性写入文件，每行一条
$file.writes(lines, "./code/a.js");
```


### add(content, path)

> 往文件末尾追加一段文字（不覆盖原有内容）。
> 
> write 会把旧内容冲掉，add 则是在文件最后面接着写。你想逐行往日志里追加记录时用它。
> 需要换行的话，自己在内容里加 "\n"。

- 参数 : content {string} 要追加的文字
- 参数 : path {string} 目标文件路径
- 版本 : 1.0.0


```javascript
// 在文件末尾追加一行文字（自己带换行符）
$file.add("我是新的内容\n", "./code/a.js");
```


### adds(lines, path)

> 把字符串数组里的每一行追加到文件末尾（自动换行）。
> 
> 和 adds 对应的单行追加不同，这里一次追加多行，而且每一行会自动换行，不需要你手写 "\n"。

- 参数 : lines {string[]} 要追加的多行内容数组
- 参数 : path {string} 目标文件路径
- 版本 : 1.0.0


```javascript
// 一次往文件末尾追加三行，自动换行
$file.adds(["追加01", "追加02", "追加03"], "./code/a.js");
```


### writeByte(bytes, path)

> 把二进制字节数组写入文件（覆盖原内容）。
> 
> 和 write 写文字对应，这里写的是原始字节，常用于把读出来的图片、音频等二进制数据另存为新文件。

- 参数 : bytes {byte[]} 要写入的字节数组
- 参数 : path {string} 目标文件路径
- 版本 : 1.0.0


```javascript
// 把一组字节写入一个文件
$file.writeByte([9, 46, 36, 7, 89, 34], "./xml/mFile.txt");
```


### copy(src, dest)

> 把一个文件复制到另一个位置。
> 
> 源文件保持不动，在目标位置生成一份一模一样的副本。源文件必须存在，否则返回 false。
> 目标路径可以是相对路径。

- 参数 : src {string} 源文件路径（要被复制的那个文件）
- 参数 : dest {string} 目标文件路径（副本放哪）
- 返回 : {boolean} 复制成功返回 true，源文件不存在或失败返回 false
- 版本 : 1.6.8


```javascript
// 把 res 目录里的 a.txt 复制到 Pictures 下的项目目录里
var ok = $file.copy("res/a.txt", "/sdcard/Pictures/测试项目/res/a.txt");
log("复制结果：" + ok);
```


### move(src, dest)

> 把文件或文件夹移动到另一个位置。
> 
> 和复制不同，移动后原来的位置就没有了。源文件/文件夹必须存在。如果目标是一个文件夹，
> 文件会被放进该文件夹里。移动成功返回 true。

- 参数 : src {string} 要移动的源文件或文件夹路径
- 参数 : dest {string} 目标位置（可以是文件夹）
- 返回 : {boolean} 移动成功返回 true，失败返回 false
- 版本 : 1.0.0


```javascript
// 把整个 modules 文件夹移动到 xml 目录下
var ok = $file.move("modules", "xml");
if (ok) {
    log("移动成功");
} else {
    log("移动失败");
}
```


### rename(src, dest)

> 给文件或文件夹改名（也可以连路径一起改，相当于移动到新路径）。
> 
> 源必须存在。它会先确保目标路径的父文件夹存在，再执行改名。成功返回 true。

- 参数 : src {string} 原来的路径
- 参数 : dest {string} 新的路径（新名字）
- 返回 : {boolean} 成功返回 true，失败返回 false
- 版本 : 1.0.0


```javascript
// 把 run.js 改名为 res/code.js
var ok = $file.rename("run.js", "res/code.js");
if (ok) {
    log("重命名成功");
} else {
    log("重命名失败");
}
```


### size(path)

> 获取文件大小（字节数）。
> 
> 返回这个文件占了多少个字节。1024 字节约等于 1 KB。如果文件不存在，返回 0。
> 想要"KB/MB"这种好看的写法，请用 sizeStr。

- 参数 : path {string} 文件路径
- 返回 : {number} 文件字节数；文件不存在时返回 0
- 版本 : 1.0.0


```javascript
// 取文件大小，单位是字节
var size = $file.size("./xml/mFile.txt");
log("文件大小：" + size + " 字节");
```


### sizeStr(size)

> 把一个字节数转换成"好看的"大小文字（自动用 B/KB/MB/GB）。
> 
> 比如 1099 字节会显示成 "1.07 KB" 这种人能看懂的写法。它不读文件，只帮你换算数字。

- 参数 : size {long} 文件字节数
- 返回 : {string} 带单位的易读大小文字，如 "6 B"、"1.07 KB"；传 null 返回 "0b"
- 版本 : 1.0.0


```javascript
// 把字节数换算成易读的大小
var s = $file.sizeStr(1099);
log(s); // 类似 "1.07 KB"
```


### sizeStr(path)

> 直接读取某个文件，并返回它"好看的"大小文字。
> 
> 相当于先 size 拿到字节数，再 sizeStr 换算。文件不存在时返回 "0b"。

- 参数 : path {string} 文件路径
- 返回 : {string} 易读大小文字，如 "6 B"；文件不存在返回 "0b"
- 版本 : 1.0.0


```javascript
// 直接得到文件的易读大小
var s = $file.sizeStr("./xml/mFile.txt");
log(s); // 类似 "6 B"
```


### name(path)

> 从一个路径里解析出"文件名"（含后缀名）。
> 
> 它不读磁盘，只是对路径字符串做切分。比如 "/sdcard/a/mFile.txt" 会得到 "mFile.txt"。

- 参数 : path {string} 文件路径
- 返回 : {string} 文件名（含后缀）
- 版本 : 1.0.0


```javascript
// 从路径里取出文件名
var fn = $file.name("/sdcard/a/mFile.txt");
log(fn); // mFile.txt
```


### mainName(path)

> 从路径里解析出"主文件名"（不含后缀名）。
> 
> 和 name 的区别：name 会带 ".txt"，mainName 把后缀去掉。比如 "mFile.txt" 得到 "mFile"。

- 参数 : path {string} 文件路径
- 返回 : {string} 不含后缀的文件名
- 版本 : 1.0.0


```javascript
// 取出不带后缀的主文件名
var fn = $file.mainName("/sdcard/a/mFile.txt");
log(fn); // mFile
```


### ext(path)

> 从路径里解析出文件后缀名（不含那个点）。
> 
> 比如 "mFile.txt" 得到 "txt"。只是字符串切分，不读磁盘。

- 参数 : path {string} 文件路径
- 返回 : {string} 后缀名（不带点）
- 版本 : 1.0.0


```javascript
// 取出后缀名
var e = $file.ext("/sdcard/a/mFile.txt");
log(e); // txt
```


### sd()

> 获取手机外部存储（SD 卡）根目录的绝对路径。
> 
> 通常返回类似 "/storage/emulated/0" 的路径。拼大路径时常用它开头。

- 返回 : {string} 外部存储根目录路径
- 版本 : 1.0.0


```javascript
// 取 SD 卡根目录路径
var path = $file.sd();
log(path); // 类似 /storage/emulated/0
```


### del(path)

> 删除文件或文件夹。
> 
> 如果删的是文件夹，会把里面的内容一起递归删掉。万一第一次没删掉，内部会自动重试最多三次。
> 不可恢复，删之前想清楚。

- 参数 : path {string} 要删除的文件或文件夹路径
- 返回 : {boolean} 删除成功返回 true，失败返回 false
- 版本 : 1.0.0


```javascript
// 删除一个文件夹
$file.del("tools");
// 删除一个文件
$file.del("main.js");
```


### ls(path)

> 列出某个文件夹里所有内容的路径。
> 
> 传入一个文件夹路径，它会返回这个文件夹里每一项（文件和子文件夹）的完整路径，装在一个数组里。
> 如果传的是脚本自带的 assets 资源路径，也能列出来。

- 参数 : path {string} 要罗列的文件夹路径
- 返回 : {list[string]} 里面每一项的完整路径组成的数组；不是文件夹时返回空数组
- 版本 : 1.6.8


```javascript
// 列出 res 文件夹里的所有项
var arr = $file.ls("res");
// 用普通 for 循环逐个打印每一条路径
for (var i = 0; i < arr.length; i++) {
    log(arr[i]);
}
```


### ls(path, filter)

> 列出文件夹内容，并按你给的过滤器筛选。
> 
> 比不带过滤器的 ls 多一步：数组里每出现一条路径，都会先调用你传入的 filter 函数问一句
> "这条要不要保留？"，返回 true 才收进结果。适合只要 .txt 文件之类的场景。

- 参数 : path {string} 要罗列的文件夹路径
- 参数 : filter {function(path){return true;}} 过滤器函数，参数是每条路径，返回 true 保留
- 返回 : {list[string]} 过滤后留下的路径数组
- 版本 : 1.6.8


```javascript
// 列出 res 下的文件，过滤器返回 true 表示全部保留
var arr = $file.ls("res", function(path) {
    return true; // 这里可以加判断，比如只保留以 .txt 结尾的
});
for (var i = 0; i < arr.length; i++) {
    log(arr[i]);
}
```


### loopFiles(path, accept)

> 递归遍历一个文件夹，把里面所有层级的文件都找出来。
> 
> ls 只看一层；loopFiles 会钻进所有子文件夹，把每一个文件都交给你。每找到一个文件，就调用
> accept 函数让你决定要不要（返回 true 保留）。返回的是 File 对象数组。

- 参数 : path {string} 要递归遍历的文件夹路径
- 参数 : accept {function(file){return true;}} 每遇到一个文件就回调，返回 true 保留
- 返回 : {File[]} 遍历得到的 File 文件对象数组
- 版本 : 1.4.9


```javascript
// 递归遍历 /res 下所有文件，这里全部保留
$file.loopFiles("/res", function(file) {
    log(file.getName()); // 打印每一个文件名
    return true;
});
```


### lsVideo()

> 查询系统媒体库中当前可见的视频信息。
> 
> 输入参数：无。返回类型为 List&lt;VideoInfo&gt;，即 Java 列表，每一项是一个 VideoInfo 信息对象。
> 用 size() 取得数量，用 get(序号) 取出一项；第一项序号是零。不能把它当作脚本数组用长度属性和方括号读取。
> 查询按加入媒体库的时间从新到旧排列，只读取系统已经收录且当前应用可见的资料，不会遍历手机里的每个目录。
> 对象记录名称、路径、字节大小和以秒为单位的加入时间；修改这些对象不会修改真实文件。
> 播放时长单位是毫秒，除以一千得到秒数。
> 安卓十三及以上入口检查读取视频权限；没有通过检查时打印提示并返回空列表。
> 安卓十二及以下入口检查读取外部存储权限。媒体库没有可见记录或没有提供查询结果时也会返回空列表。
> 系统查询异常会向外抛出；下面用异常处理展示如何记录失败，空列表不一定表示手机没有这种文件。

- 返回 : {List<VideoInfo>} 视频信息列表；数量为零时不要取第一项
- 版本 : 1.5.4


```javascript
try {
    // 先在设备上授予相应读取权限，再查询列表。
    var list = $file.lsVideo();
    if (list == null || list.size() === 0) {
        log("没有可读取的视频记录，请检查权限和媒体库内容。");
    } else {
        // 逐项读取信息：序号从零开始，不超过列表数量。
        for (var index = 0; index < list.size(); index++) {
            var info = list.get(index); // 得到一个 VideoInfo 对象。
            log("名称：" + info.getName());
            log("路径：" + info.getPath());
            log("大小（字节）：" + info.getSize());
            log("时长（秒）：" + Number(info.getDur()) / 1000);
            // 媒体库保存秒数；脚本日期对象需要毫秒。
            log(new Date(Number(info.getTime()) * 1000).toString());
        }
    }
} catch (error) {
    log("查询视频信息失败：" + error);
}
```


### lsAudio()

> 查询系统媒体库中当前可见的音频信息。
> 
> 输入参数：无。返回类型为 List&lt;AudioInfo&gt;，即 Java 列表，每一项是一个 AudioInfo 信息对象。
> 用 size() 取得数量，用 get(序号) 取出一项；第一项序号是零。不能把它当作脚本数组用长度属性和方括号读取。
> 查询按加入媒体库的时间从新到旧排列，只读取系统已经收录且当前应用可见的资料，不会遍历手机里的每个目录。
> 对象记录名称、路径、字节大小和以秒为单位的加入时间；修改这些对象不会修改真实文件。
> 播放时长单位是毫秒，除以一千得到秒数。
> 安卓十三及以上入口检查读取音频权限；没有通过检查时打印提示并返回空列表。
> 安卓十二及以下入口检查读取外部存储权限。媒体库没有可见记录或没有提供查询结果时也会返回空列表。
> 系统查询异常会向外抛出；下面用异常处理展示如何记录失败，空列表不一定表示手机没有这种文件。

- 返回 : {List<AudioInfo>} 音频信息列表；数量为零时不要取第一项
- 版本 : 1.5.4


```javascript
try {
    // 先在设备上授予相应读取权限，再查询列表。
    var list = $file.lsAudio();
    if (list == null || list.size() === 0) {
        log("没有可读取的音频记录，请检查权限和媒体库内容。");
    } else {
        // 逐项读取信息：序号从零开始，不超过列表数量。
        for (var index = 0; index < list.size(); index++) {
            var info = list.get(index); // 得到一个 AudioInfo 对象。
            log("名称：" + info.getName());
            log("路径：" + info.getPath());
            log("大小（字节）：" + info.getSize());
            log("时长（秒）：" + Number(info.getDur()) / 1000);
            // 艺术家和专辑可能为空，不要假设每条记录都填写了。
            log("艺术家：" + info.getArtist());
            log("专辑：" + info.getAlbum());
            // 媒体库保存秒数；脚本日期对象需要毫秒。
            log(new Date(Number(info.getTime()) * 1000).toString());
        }
    }
} catch (error) {
    log("查询音频信息失败：" + error);
}
```


### lsImages()

> 查询系统媒体库中当前可见的图片信息。
> 
> 输入参数：无。返回类型为 List&lt;ImageInfo&gt;，即 Java 列表，每一项是一个 ImageInfo 信息对象。
> 用 size() 取得数量，用 get(序号) 取出一项；第一项序号是零。不能把它当作脚本数组用长度属性和方括号读取。
> 查询按加入媒体库的时间从新到旧排列，只读取系统已经收录且当前应用可见的资料，不会遍历手机里的每个目录。
> 对象记录名称、路径、字节大小和以秒为单位的加入时间；修改这些对象不会修改真实文件。
> 还可以读取宽度和高度，单位是像素；返回的是图片资料，不是已经解码的图像。
> 当前实现的权限检查有特殊之处：在安卓十三及以上，入口检查的是读取视频权限，而随后查询的是图片库。
> 因此仅授予图片权限仍可能在入口取得空列表，通过入口检查也不代表图片查询一定成功。请结合实际授权范围判断结果。
> 安卓十二及以下入口检查读取外部存储权限。媒体库没有可见记录或没有提供查询结果时也会返回空列表。
> 系统查询异常会向外抛出；下面用异常处理展示如何记录失败，空列表不一定表示手机没有这种文件。

- 返回 : {List<ImageInfo>} 图片信息列表；数量为零时不要取第一项
- 版本 : 1.5.4


```javascript
try {
    // 先在设备上授予相应读取权限，再查询列表。
    var list = $file.lsImages();
    if (list == null || list.size() === 0) {
        log("没有可读取的图片记录，请检查权限和媒体库内容。");
    } else {
        // 逐项读取信息：序号从零开始，不超过列表数量。
        for (var index = 0; index < list.size(); index++) {
            var info = list.get(index); // 得到一个 ImageInfo 对象。
            log("名称：" + info.getName());
            log("路径：" + info.getPath());
            log("大小（字节）：" + info.getSize());
            log("尺寸（像素）：" + info.getWidth() + " × " + info.getHeight());
            // 媒体库保存秒数；脚本日期对象需要毫秒。
            log(new Date(Number(info.getTime()) * 1000).toString());
        }
    }
} catch (error) {
    log("查询图片信息失败：" + error);
}
```


### getDir(name, isPublic)

> 获取安卓系统常用目录（图片、下载、音乐、视频等）的路径。
> 
> 你传一个目录类型名字，它就返回对应目录的绝对路径。常见取值有：图片、下载、dcim、音乐、
> 视频、文档、闹钟、通知、播客、铃声。第二个参数控制要"公共目录"还是"应用私有目录"。
> 如果传的名字不在这些常见类型里，就当成自定义目录名，返回应用内部私有目录。

- 参数 : name {string} 目录类型名，如 "图片"、"下载"、"音乐"、"视频"、"dcim"
- 参数 : isPublic {boolean} true 取公共目录，false 取应用私有目录；传 null 按 true 处理
- 返回 : {string} 对应目录的绝对路径；name 为 null 时返回 null
- 版本 : 1.6.1


```javascript
// 取公共的"视频"目录路径
var videoPath = $file.getDir("视频", true);
log(videoPath);
```


### getDir(name)

> 获取安卓"公共目录"的路径（默认取公共目录版本）。
> 
> 和两个参数的版本一样，只是省掉第二个参数，默认按公共目录处理。

- 参数 : name {string} 目录类型名，如 "图片"、"下载"、"视频"
- 返回 : {string} 对应公共目录的绝对路径
- 版本 : 1.6.1


```javascript
// 取公共"视频"目录路径
var videoPath = $file.getDir("视频");
log(videoPath);
```


### flushSd(successCallback, failCallback)

> 刷新整个外部存储的媒体库，让系统立刻识别新写入的文件。
> 
> 你用脚本往相册目录写了一张图后，系统相册可能要过一会儿才看得见。调用本方法会通知媒体库
> 重新扫描。扫描完成后会回调 successCallback；失败回调 failCallback。

- 参数 : successCallback {function()} 刷新成功后回调
- 参数 : failCallback {function()} 刷新失败后回调
- 版本 : 1.9.5


```javascript
// 刷新 SD 卡媒体库，完成后打印日志
$file.flushSd(function() {
    log("刷新成功");
}, function() {
    log("刷新失败");
});
```


### flush(filePath, successCallback, failCallback)

> 刷新某一个具体文件，让系统媒体库立刻识别它。
> 
> 和刷新整个 SD 卡不同，这里只通知系统扫描你指定的那一个文件（比如刚保存的图片），
> 扫描完回调 successCallback，失败回调 failCallback。

- 参数 : filePath {String} 要刷新的文件路径
- 参数 : successCallback {function()} 成功后回调
- 参数 : failCallback {function()} 失败后回调
- 版本 : 1.9.5


```javascript
// 让系统立刻识别刚保存的这张图片
$file.flush("/sdcard/Pictures/sample.png", function() {
    log("刷新成功");
}, function() {
    log("刷新失败");
});
```


### hotUpdate(path, data)

> 写入一个"热更新"文件：以后脚本读这个相对路径时会优先用你这里写的内容。
> 
> 作用是不重新打包 App，也能临时替换某个资源文件的内容。传入的是相对路径和新内容，
> 系统会把它存到热更新目录；之后脚本用到该相对路径时优先读它。

- 参数 : path {String} 要热更新的相对路径
- 参数 : data {String} 新的文件内容
- 版本 : 1.9.6


```javascript
// 把 sample 这个相对路径的内容热更新为 "sample text"
$file.hotUpdate("/sdcard/Pictures/sample.png", "sample text");
```


### delHotUpdate(path)

> 删除某个相对路径的热更新文件。
> 
> 因为系统会优先读热更新文件，如果项目本身的文件已经更新，但热更新目录里还留着旧的同名文件，
> 就会一直读到旧的。这时调用本方法把热更新删掉，让它恢复读正式文件。

- 参数 : path {String} 要删除热更新的相对路径
- 版本 : 1.9.6


```javascript
// 删除 sample 对应的热更新文件
$file.delHotUpdate("/sdcard/Pictures/sample.png");
```


### reext(src, newExt)

> 修改文件的后缀名（把 a.txt 改成 a.md 这种）。
> 
> 它保留原来的文件夹和主文件名，只换后缀。如果原文件本来没有后缀，就相当于给它追加一个后缀。
> 源文件必须存在，新后缀不能为空。

- 参数 : src {String} 源文件路径
- 参数 : newExt {String} 新的后缀名（不要带那个点）
- 返回 : {boolean} 成功返回 true，源文件不存在或新后缀为空返回 false
- 版本 : 2.0.2


```javascript
// 把 sample 文件的后缀改成 sample（即改名为 xxx.sample）
var result = $file.reext("sample", "sample");
log("改后缀结果：" + result);
```


### getParent(src)

> 取一个文件路径的"上一层目录"。
> 
> 比如路径是 "/sdcard/dir/love.txt"，父目录就是 "/sdcard/dir"。路径必须真实存在，
> 不存在时返回 null。

- 参数 : src {String} 文件路径
- 返回 : {String} 上一层目录路径；文件不存在返回 null
- 版本 : 2.0.2


```javascript
// 取上一层目录
var path = "/sdcard/dir/love.txt";
var parent = $file.getParent(path);
log(parent); // 结果：/sdcard/dir
```


