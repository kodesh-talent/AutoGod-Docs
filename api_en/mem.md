# $mem - 内存读写库

- 更新时间:2026-10-22 10:56:35

> 内存读写库
> 
> 可以把它理解成一个“遥控器”：先用 init(int, int) 连上目标进程，
> 连上之后才能做读取、写入、扫描、打补丁、转储这些事。
> 操作自己所在的进程不需要 Root；操作别的 App 的进程需要 Root 或者 ptrace 权限，
> 否则连接会直接失败。
> 
> 本类所有方法的返回值都是 JSON 字符串，拿到结果后第一件事就是看 ok 字段：
> ok 为 true 表示成功，结果数据放在同级的其它字段里；
> ok 为 false 表示失败，失败原因写在 error 字段里。
> 
> 新手最容易踩的三个坑：
> 一、没连接进程就直接读写，会返回“尚未连接进程”；
> 二、地址写错（比如忘记写 L 后缀、或者拷贝了十进制数），读写会失败甚至让目标崩溃；
> 三、用完补丁、备份、ptrace 没有恢复或分离，会把目标进程卡住。



```javascript
// 第一步：先看看原生库是否加载成功
let loaded = $mem.isSoLoad();
// 第二步：连接自己所在的进程，syscall 表示用系统调用方式读写
let connect = $mem.init(android.os.Process.myPid(), $mem.syscall);
// 第三步：读取目标地址开始的 16 个字节，第三个参数 true 表示跳过不可读的内存页
let hex = $mem.read(0x7f00000000L, 16, true);
```




### const {int} syscall;

> 内存读写方式一：系统调用。
> 
> 走 process_vm_readv / process_vm_writev 这两个内核接口，速度快、开销小，
> 不需要 Root 也能用，但是部分厂商内核把它关掉了，这个时候请换成
> proc}。

- 版本 : 2.0.3


```javascript
// 优先用系统调用方式连接目标进程
let json = $mem.init(pid, $mem.syscall);
```


### const {int} proc;

> 内存读写方式二：/proc 内存文件。
> 
> 走 /proc/目标PID/mem 这个文件读写，兼容性最好，几乎所有内核都支持，
> 缺点是需要 Root 或足够权限，而且比系统调用方式慢一些。

- 版本 : 2.0.3


```javascript
// 当系统调用方式连不上时，换成读写 /proc/<pid>/mem 的方式
let json = $mem.init(pid, $mem.proc);
```


### const {int} arm32;

> 处理器架构一：32 位 ARM（armeabi-v7a）。
> 
> 只有 createPatch(long, String, int, boolean) 在写汇编补丁时才用到，
> 32 位 ARM 设备传这个值。

- 版本 : 2.0.3


### const {int} arm64;

> 处理器架构二：64 位 ARM（arm64-v8a）。
> 
> 现在绝大多数手机都是这个架构，写汇编补丁时传这个值。

- 版本 : 2.0.3


### const {int} x86;

> 处理器架构三：32 位 x86。
> 
> 老式模拟器或部分 x86 平板使用这个架构，写汇编补丁时传这个值。

- 版本 : 2.0.3


### const {int} x86_64;

> 处理器架构四：64 位 x86（x86_64）。
> 
> 电脑上的安卓模拟器多数是这个架构，写汇编补丁时传这个值。

- 版本 : 2.0.3


### isSoLoad()

> 原生库是否已加载成功。
> 
> 这是排查问题的第一步：只有它为 true，后面的读写能力才谈得上。
> 如果返回 false，立刻用 getLoadError() 拿到失败原因，
> 常见原因是 APK 里打进了不匹配的 ABI，或者设备架构不在支持范围内。

- 返回 : {boolean} true 表示原生库已经加载成功；false 表示加载失败
- 版本 : 2.0.3


```javascript
// 先判断原生库能不能用，不能用的话后面的调用全是空转
if (!$mem.isSoLoad()) {
    // 打印出加载失败的原因
    $log.e("demo", $mem.getLoadError());
    return;
}
```


### getLoadError()

> 原生库加载失败的原因。
> 
> 和 isSoLoad() 配套使用：
> 加载成功时返回 null，加载失败时返回具体的失败说明，
> 例如找不到文件、ABI 不匹配、依赖缺失等。

- 返回 : {string} 加载失败的原因说明；加载成功时为 null
- 版本 : 2.0.3


```javascript
// 加载正常时这里拿到的是 null
let reason = $mem.getLoadError();
if (reason != null) {
    // 把原因显示给用户看，方便定位是哪种设备不支持
    $log.e("demo", "原生库加载失败：" + reason);
}
```


### info()

> 获取运行环境信息（跑通环境的第一个检查项）。
> 
> 返回当前原生库的 ABI、系统 SDK 版本、自身进程号、用户 ID、是否 Root 等信息，
> 出问题时先把这份数据发给排查者，可以快速判断是环境不支持还是权限不够。
> 
> 这个方法不需要先连接进程，随时都能调用。

- 返回 : {string} JSON 字符串，形如 {"ok":true,"abi":"arm64-v8a","sdk":33,"pid":1234,"uid":10123,"root":false,"keystone":true,"library":"_mem"}
- 版本 : 2.0.3


```javascript
// 查看 abi（架构）、sdk（系统版本）、pid（进程号）、root（是否有超级权限）
let info = $mem.info();
```


### selfTest()

> 自检本机能力（判断这台设备能不能用的最快方式）。
> 
> 会在自己进程里真刀真枪地跑一遍：两种内存方式、读写、备份、补丁、扫描、ELF、指针校验、汇编。
> 哪一项是 false，就说明这项能力在当前设备上不可用，需要换方式或者换设备。
> 
> 这个方法不需要先连接进程，随时都能调用。

- 返回 : {string} JSON 字符串，形如 {"ok":true,"syscall":true,"procMem":true,"readWrite":true,"backup":true,"patchRestore":true,"patternScan":true,"elfScan":true,"pointerValidation":true,"keystoneAssembly":true}
- 版本 : 2.0.3


```javascript
// 挨个功能做一次体检
let result = $mem.selfTest();
// 结果里 syscall、procMem、readWrite、patchRestore 等字段，false 就是那一关没过
```


### lsProc()

> 列出可见进程（找目标 PID 用）。
> 
> 扫描 /proc 目录，把当前权限范围内能看到的进程号和进程名都列出来。
> 拿到 PID 之后才能用 init(int, int) 去连接。
> 
> 注意：安卓 8.0 以后很多进程名已经读不到了，看不到不代表进程不存在。

- 返回 : {string} JSON 字符串，形如 {"ok":true,"processes":[{"pid":1234,"name":"top.kodesh.app.mem"}]}；读取失败时形如 {"ok":false,"error":"无法读取 /proc"}
- 版本 : 2.0.3


```javascript
// 先列出进程，拿到想要操作的那个进程号
let json = $mem.lsProc();
// 结果形如 {"ok":true,"processes":[{"pid":1234,"name":"top.kodesh.app.mem"}]}
```


### init(pid, mode)

> 连接目标进程（所有内存操作的第一步）。
> 
> 连上之后，后续所有读写、扫描、补丁都针对这个进程。
> 重复调用会先清空旧的补丁和备份句柄，所以重新连接前请把之前保存的句柄丢掉。
> 
> 连接自己的进程一般能成功；连接别人的进程需要 Root 或 ptrace 权限，
> 失败时请检查 SELinux、权限和目标进程是否存在。

- 参数 : pid {int} 目标进程的进程号，可以从 lsProc() 里拿到；传错会直接连接失败
- 参数 : mode {int} 读写方式，填 syscall} 或 proc}；填其它值按系统调用处理
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"pid":1234,"name":"目标进程名"}；失败形如 {"ok":false,"error":"初始化失败，请确认目标进程存在且当前进程有访问权限"}
- 版本 : 2.0.3


```javascript
// 用系统调用方式连接指定进程，绝大多数情况先用这个
let json = $mem.init(pid, $mem.syscall);
// 如果上面连接失败，再换成读写 /proc/<pid>/mem 的方式试一次
let json2 = $mem.init(pid, $mem.proc);
```


### lsMap(filter)

> 列出目标进程的内存映射（找可读范围用）。
> 
> 映射就是进程把文件、堆、栈、动态库“贴”到自己地址空间的每一块，
> 只有落在可读映射里的地址才能读，只有落在可写映射里的地址才能写。
> 所以扫描和读写之前，先读这份列表确认范围，能少踩很多坑。
> 
> 前提：必须先 init(int, int) 连上进程。

- 参数 : filter {string} 路径过滤关键字，填 null 或空串表示全部列出；只保留路径里包含该关键字的映射
- 返回 : {string} JSON 字符串，形如 {"ok":true,"total":120,"maps":[{"start":"0x7f0000","end":"0x7f1000","size":4096,"perms":"r-xp","path":"/system/lib64/libc.so"}]}；未连接时形如 {"ok":false,"error":"尚未连接进程"}
- 版本 : 2.0.3


```javascript
// 列出全部映射，重点看 perms 字段有没有 r（可读）或 w（可写）
let all = $mem.lsMap("");
// 只看某个动态库的映射，第二个参数按路径包含关系过滤
let one = $mem.lsMap("lib_mem.so");
```


### lsElf()

> 列出目标进程已加载的 ELF 文件（找动态库基址用）。
> 
> ELF 就是 .so 动态库文件的格式。这里会把进程加载过的所有动态库的
> 起始地址、结束地址、大小和完整路径列出来，
> 拿到基址之后加上符号偏移，就能定位到具体的函数或变量。
> 
> 前提：必须先 init(int, int) 连上进程。

- 返回 : {string} JSON 字符串，形如 {"ok":true,"count":50,"elfs":[{"base":"0x7f0000","end":"0x7f8000","size":32768,"path":"/system/lib64/libc.so"}]}；未连接时形如 {"ok":false,"error":"尚未连接进程"}
- 版本 : 2.0.3


```javascript
// 看看目标进程加载了哪些 so 文件，各自贴在哪个地址上
let json = $mem.lsElf();
// 结果形如 {"ok":true,"count":50,"elfs":[{"base":"0x7f0000","end":"0x7f8000","size":32768,"path":"/system/lib64/libc.so"}]}
```


### read(address, length, skipInaccessiblePages)

> 按字节读取内存（原样取数据，结果转成 HEX）。
> 
> 这是最常用的读取方法，把目标地址开始的若干字节读出来，
> 结果以两位十六进制、空格分隔的形式返回，方便人眼看和后续处理。
> 
> 前提：必须先 init(int, int) 连上进程。
> 注意：长度限制为 1 到 1 MiB（1048576 字节），超过会直接失败。

- 参数 : address {long} 要读取的起始地址，必须是目标进程里的有效虚拟地址；写完之后记得加 L 后缀
- 参数 : length {int} 要读取的字节数，范围 1 到 1048576
- 参数 : skipInaccessiblePages {boolean} 是否跳过不可读的内存页；true 能读完大范围里读不到的地方，false 遇到不可读页就直接返回已读到的部分
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"bytes":16,"hex":"7f 45 4c 46"}；失败形如 {"ok":false,"error":"地址或长度无效（最大 1 MiB）"}
- 版本 : 2.0.3


```javascript
// 读取 16 个字节，第三个参数 true 表示遇到不可读的页就跳过去继续读
let json = $mem.read(0x7f00000000L, 16, true);
// 结果形如 {"ok":true,"bytes":16,"hex":"7f 45 4c 46 02 01 01 00"}
```


### write(address, hex)

> 按 HEX 写入内存（改数值、改标志位用）。
> 
> 传入十六进制文本，会被转成字节写入目标地址。
> 写入前建议先 checkPointer(long, int) 确认这块地址可写，
> 并且先 createBackup(long, int) 备份原始数据，写错了还能还原。
> 
> 前提：必须先 init(int, int) 连上进程。
> 注意：HEX 文本长度必须是偶数，空格会被自动忽略。

- 参数 : address {long} 要写入的目标地址，必须是可写的虚拟地址
- 参数 : hex {string} 十六进制数据，必须是偶数位，支持空格分隔，例如 "90 90" 或 "9090"
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"bytes":4}；失败形如 {"ok":false,"error":"地址或十六进制数据无效"}
- 版本 : 2.0.3


```javascript
// 写入 4 个字节，空格只是为了方便看，写的时候会被自动忽略
let json = $mem.write(0x7f00000000L, "01 02 03 04");
// 结果形如 {"ok":true,"bytes":4}
```


### readStr(address, maxLength)

> 按 UTF-8 读取字符串（读文本用）。
> 
> 从目标地址开始读，一直读到字符串结尾的 0 字节或者达到最大长度为止。
> 只适合读文本；读二进制数据请一律用 read(long, int, boolean)}。
> 
> 前提：必须先 init(int, int) 连上进程。

- 参数 : address {long} 字符串的起始地址
- 参数 : maxLength {int} 最多读取的字节数，范围 1 到 1048576；达到上限还没遇到结尾就截断
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"value":"Hello","bytes":5}；失败形如 {"ok":false,"error":"地址或最大长度无效"}
- 版本 : 2.0.3


```javascript
// 最多读 64 个字节，遇到结尾 0 就自动停下
let json = $mem.readStr(0x7f00000000L, 64);
// 结果形如 {"ok":true,"value":"Hello","bytes":5}
```


### writeStr(address, value)

> 按 UTF-8 写入字符串（改文本内容用）。
> 
> 写入时会自动在末尾补一个 0 作为字符串结尾，
> 所以目标位置必须比字符串本身多留出 1 个字节的空间，
> 否则会踩到后面的数据，导致目标进程崩溃。
> 
> 前提：必须先 init(int, int) 连上进程。

- 参数 : address {long} 要写入的目标地址，必须可写，并且要预留出额外的 1 个字节
- 参数 : value {string} 要写入的文本内容，按 UTF-8 编码写入
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"bytes":6}；失败形如 {"ok":false,"error":"字符串写入失败"}
- 版本 : 2.0.3


```javascript
// 写 5 个英文字符，加上自动补的结尾，一共占用 6 个字节
let json = $mem.writeStr(0x7f00000000L, "Hello");
// 结果形如 {"ok":true,"bytes":6}
```


### scanPattern(start, end, idaPattern, resultLimit)

> 按特征码扫描内存（定位代码或数据用）。
> 
> 所谓 IDA 特征码，就是用十六进制描述一段规律字节，
> 例如 "7F 45 4C 46"，其中两个 question 号 "??" 代表“这一位是什么都行”。
> 适合用来在版本更新后重新定位一段代码或一段数据。
> 
> 前提：必须先 init(int, int) 连上进程。
> 注意：扫描范围请从 lsMap(String) 里取，范围越大越慢。

- 参数 : start {long} 扫描起始地址，必须大于 0
- 参数 : end {long} 扫描结束地址，必须大于起始地址
- 参数 : idaPattern {string} IDA 风格特征码，十六进制字节之间用空格隔开，"??" 表示通配该字节
- 参数 : resultLimit {int} 最多返回多少个结果地址，不足 1 时按 1 处理
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"count":2,"addresses":["0x7f00001000"]}；失败形如 {"ok":false,"error":"扫描范围无效"}
- 版本 : 2.0.3


```javascript
// 在一段范围里找 ELF 文件头，最多返回 200 个结果
let json = $mem.scanPattern(0x7f00000000L, 0x7f01000000L, "7F 45 4C 46", 200);
// 中间两位不确定的写法，用 ?? 当通配符
let json2 = $mem.scanPattern(0x7f00000000L, 0x7f01000000L, "7F ?? ?? 46", 200);
// 结果形如 {"ok":true,"count":2,"addresses":["0x7f00001000","0x7f00008000"]}
```


### createPatch(address, code, architecture, assembly)

> 创建并立即生效补丁（改逻辑指令用）。
> 
> 补丁就是把目标地址的那几个字节替换掉。最后一个参数为 true 时，
> 传入的内容会被当成汇编代码，由 Keystone 现翻成机器码，省得自己手算机器码；
> 为 false 时按 HEX 直接写入。
> 
> 前提：必须先 init(int, int) 连上进程。
> 重要：成功后一定要记下返回的 handle，并在用完之后调用 restorePatch(long) 还原，
> 建议把恢复写在 finally 里，否则目标进程会一直运行被改过的代码。

- 参数 : address {long} 要打补丁的指令地址，通常是代码段里的一条指令开始处
- 参数 : code {string} 补丁内容；assembly 为 true 时写汇编语句（多条用分号隔开），为 false 时写 HEX
- 参数 : architecture {int} 目标处理器架构，填 arm32}、arm64}、x86} 或 x86_64}
- 参数 : assembly {boolean} true 表示把 code 当成汇编处理；false 表示把 code 当成 HEX 处理
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"handle":1,"original":"48 89","current":"90 90"}；失败形如 {"ok":false,"error":"补丁创建失败；IO 内存访问权限不足或输入无效"}
- 版本 : 2.0.3


```javascript
// 方式一：直接按机器码打补丁，90 是 x86 架构的空指令 nop
let hexPatch = $mem.createPatch(0x7f00000000L, "90 90", $mem.x86_64, false);
// 方式二：写汇编语句，由底层自动翻译成机器码，可读性更好
let asmPatch = $mem.createPatch(0x7f00000000L, "mov eax, 1; ret", $mem.x86_64, true);
// 两种写法返回都一样，形如 {"ok":true,"handle":1,"original":"48 89","current":"90 90"}，handle 要留着用来恢复
```


### restorePatch(handle)

> 还原并释放补丁句柄（务必成对调用）。
> 
> 把 createPatch(long, String, int, boolean) 改掉的字节写回原样，并把这个句柄释放掉。
> 同一个句柄重复恢复会失败，因为还原成功之后句柄就被删掉了。
> 
> 强烈建议放在 finally 代码块里调用，保证异常发生时也一定能还原。

- 参数 : handle {long} 补丁句柄，来自 createPatch(long, String, int, boolean) 返回值里的 handle 字段
- 返回 : {string} JSON 字符串，成功形如 {"ok":true}；失败形如 {"ok":false,"error":"补丁句柄不存在"} 或 {"ok":false,"error":"恢复补丁失败"}
- 版本 : 2.0.3


```javascript
// 打完补丁、做完验证之后，第一时间把代码还原回去
let json = $mem.restorePatch(handle);
// 推荐写法：无论中间有没有报错，最后都会执行还原
try {
    $mem.createPatch(address, "90", $mem.x86_64, false);
} finally {
    $mem.restorePatch(handle);
}
```


### createBackup(address, length)

> 备份一段原始内存（动手改之前先留后路）。
> 
> 只把原始字节抄下来保存，不会改动目标内存，非常安全。
> 之后随时可以用 restoreBackup(long) 把数据写回去。
> 
> 前提：必须先 init(int, int) 连上进程。
> 注意：句柄保存在底层 C++ 里，进程被杀或者重新 init(int, int) 都会失效。

- 参数 : address {long} 要备份的起始地址
- 参数 : length {int} 要备份的字节数
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"handle":2,"original":"48 89 65 f8"}；失败形如 {"ok":false,"error":"备份创建失败"}
- 版本 : 2.0.3


```javascript
// 把目标位置的 8 个字节先抄一份留底
let json = $mem.createBackup(0x7f00000000L, 8);
// 结果形如 {"ok":true,"handle":2,"original":"48 89 65 f8 48 8b 45 f0"}，handle 要保存好
```


### restoreBackup(handle)

> 用备份还原内存并释放句柄。
> 
> 把 createBackup(long, int) 抄下来的原始字节写回目标进程，
> 写完之后这个句柄也会被释放，不能重复还原同一个句柄。

- 参数 : handle {long} 备份句柄，来自 createBackup(long, int) 返回值里的 handle 字段
- 返回 : {string} JSON 字符串，成功形如 {"ok":true}；失败形如 {"ok":false,"error":"备份句柄不存在"} 或 {"ok":false,"error":"恢复备份失败"}
- 版本 : 2.0.3


```javascript
// 改完验证不通过，就用备份把内存还原成原来的样子
let json = $mem.restoreBackup(handle);
// 成功返回 {"ok":true}；句柄不存在返回 {"ok":false,"error":"备份句柄不存在"}
```


### findSymbol(elfName, symbolName)

> 查找动态符号地址（调用函数前的必经一步）。
> 
> 在指定的动态库里查找导出符号的地址，拿到地址之后才能用
> remoteCall(long, long[]) 去调用它。
> 
> 前提：必须先 init(int, int) 连上进程。
> 注意：elfName 用 lsElf() 里列出来的文件名；符号必须在导出表里才找得到。

- 参数 : elfName {string} 动态库文件名，例如 "libc.so"、"lib_mem.so"，支持路径片段
- 参数 : symbolName {string} 要查找的动态符号名，例如 "open"、"JNI_OnLoad"
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"address":"0x7f12345000"}；失败形如 {"ok":false,"error":"未找到 ELF"} 或 {"ok":false,"error":"未找到符号"}
- 版本 : 2.0.3


```javascript
// 在 libc.so 里查找 open 函数的地址
let json = $mem.findSymbol("libc.so", "open");
// 结果形如 {"ok":true,"address":"0x7f12345000"}
```


### dumpRange(start, end, destination)

> 把一段地址范围导出成文件（抓包式的原始取证）。
> 
> 把起止地址之间的内存内容原样写进目标文件，方便用十六进制编辑器慢慢分析。
> 
> 前提：必须先 init(int, int) 连上进程。
> 注意：范围要从 lsMap(String) 里挑可读的部分，路径要在有写权限的目录下，比如应用自己的私有目录。

- 参数 : start {long} 起始地址（包含）
- 参数 : end {long} 结束地址（不包含）
- 参数 : destination {string} 要写成的文件路径，所在的文件夹必须存在且有写权限
- 返回 : {string} JSON 字符串，成功形如 {"ok":true}；失败形如 {"ok":false,"error":"转储失败"}
- 版本 : 2.0.3


```javascript
// 把一段地址范围导出到自己的私有目录
let json = $mem.dumpRange(0x7f00000000L, 0x7f01000000L, getFilesDir() + "/dump.bin");
// 成功返回 {"ok":true}；失败返回 {"ok":false,"error":"转储失败"}
```


### dumpMap(mappedFile, destination)

> 把某个映射文件的内存导出成文件。
> 
> 按“映射文件名”一次性导出它对应的全部内存，
> 比 dumpRange(long, long, String) 省事，不用自己算起止地址。
> 
> 前提：必须先 init(int, int) 连上进程。

- 参数 : mappedFile {string} 映射文件路径或文件名，支持路径片段，例如 "libc.so"
- 参数 : destination {string} 要写成的文件路径，所在的文件夹必须存在且有写权限
- 返回 : {string} JSON 字符串，成功形如 {"ok":true}；失败形如 {"ok":false,"error":"映射文件转储失败"}
- 版本 : 2.0.3


```javascript
// 把整个 libc.so 的内存内容导出到文件（不是导出磁盘上的原文件）
let json = $mem.dumpMap("libc.so", getFilesDir() + "/libc.bin");
// 成功返回 {"ok":true}；失败返回 {"ok":false,"error":"映射文件转储失败"}
```


### dumpElf(elfName, destination)

> 把目标进程里的某个动态库导出成文件。
> 
> 和 dumpMap(String, String) 的区别是：
> 这个按 ELF 结构导出，更适合拿来直接与反汇编工具里的结果对照。
> 
> 前提：必须先 init(int, int) 连上进程。

- 参数 : elfName {string} 动态库文件名或路径片段，例如 "lib_mem.so"
- 参数 : destination {string} 要写成的文件路径，所在的文件夹必须存在且有写权限
- 返回 : {string} JSON 字符串，成功形如 {"ok":true}；失败形如 {"ok":false,"error":"未找到 ELF"} 或 {"ok":false,"error":"ELF 转储失败"}
- 版本 : 2.0.3


```javascript
// 导出目标进程里的 lib_mem.so
let json = $mem.dumpElf("lib_mem.so", context.getFilesDir() + "/mem.so");
// 成功返回 {"ok":true}；找不到文件时返回 {"ok":false,"error":"未找到 ELF"}
```


### trace(attach)

> ptrace 附加或分离（远程调用和单步的前置动作）。
> 
> 附加就是让当前进程“盯上”目标进程的线程，只有附加成功之后，
> 才能做 traceControl(int, int) 单步、远程调用函数等高级操作。
> 
> 前提：必须先 init(int, int) 连上进程。
> 重要：用完一定要传 false 分离，否则目标进程会一直被挂住。

- 参数 : attach {boolean} true 表示附加到目标进程；false 表示从目标进程分离
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"attached":true}；失败形如 {"ok":false,"error":"ptrace attach 失败"} 或 {"ok":false,"error":"ptrace detach 失败"}
- 版本 : 2.0.3


```javascript
// 先附加，传 true
let attached = $mem.trace(true);
// 结果形如 {"ok":true,"attached":true}
// 做完事情之后，传 false 分离，建议写在 finally 里保证一定执行
let detached = $mem.trace(false);
```


### traceControl(operation, value)

> 执行 ptrace 控制操作（调试目标进程的总开关）。
> 
> 这一个方法集成了附加、抢占附加、分离、暂停、继续、单步等多种控制能力，
> 靠 operation 数字来区分要做什么。
> 
> 前提：必须先 init(int, int) 连上进程。

- 参数 : operation {int} 控制类型：0 附加、1 抢占式附加、2 分离、3 停止、4 继续、5 单步、6 等待单步、7 等待系统调用；除 2、3、7 外都需要配合 value
- 参数 : value {int} 附加的线程号、单步步数、继续时的信号等；最小值会被自动抬到 1
- 返回 : {string} JSON 字符串，成功形如 {"ok":true}；失败形如 {"ok":false,"error":"未知 trace 操作"} 或 {"ok":false,"error":"trace 操作失败"}
- 版本 : 2.0.3


```javascript
// operation 填 3：停下来（暂停目标进程）
let stop = $mem.traceControl(3, 0);
// operation 填 4：继续跑（恢复目标进程）
let cont = $mem.traceControl(4, 0);
// operation 填 6：单步一次，value 表示步数
let step = $mem.traceControl(6, 1);
```


### remoteCall(functionAddress, arguments)

> 在目标进程里调用函数（让目标替你干活）。
> 
> 已经附加之后，可以直接让目标进程执行某个函数。
> 函数地址一般先用 findSymbol(String, String) 查出来。
> 
> 前提：必须先 trace(boolean) 附加成功。
> 危险：调用约定、参数个数弄错，大概率会把目标进程搞崩，务必先小范围验证。

- 参数 : functionAddress {long} 要调用的函数地址，通常来自 findSymbol(String, String)}
- 参数 : arguments {long[]} 参数数组，最多取前 6 个元素；没有参数时传空数组
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"result":"0x7f12346000"}；失败形如 {"ok":false,"error":"远程函数调用失败"}
- 版本 : 2.0.3


```javascript
// 最多支持 6 个参数，不够用时前面几个先传进去即可
let args = [句柄值, 缓冲区地址, 长度];
let json = $mem.remoteCall(0x7f12345000L, args);
// 结果形如 {"ok":true,"result":"0x7f12346000"}，result 是函数返回值
```


### remoteSyscall(syscallNumber, arguments)

> 在目标进程里执行系统调用。
> 
> 绕过 Java 层，直接让目标进程执行一条原生 syscall。
> 系统调用号请使用十进制，不需要写成 0x 开头的十六进制。
> 
> 前提：必须先 trace(boolean) 附加成功。
> 危险：调用号和参数个数必须和目标 CPU 架构、ABI 完全对得上，填错会直接搞崩目标进程。

- 参数 : syscallNumber {long} 系统调用号，必须符合目标进程所在 CPU 架构的编号表
- 参数 : arguments {long[]} 参数数组，最多取前 6 个元素；没有参数时传空数组
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"result":"0x0"}；失败形如 {"ok":false,"error":"远程系统调用失败"}
- 版本 : 2.0.3


```javascript
// syscall 编号用十进制，最多支持 6 个参数
let args = [1, 2, 3];
let json = $mem.remoteSyscall(63L, args);
// 结果形如 {"ok":true,"result":"0x0"}
```


### lsThread()

> 列出目标进程的线程号。
> 
> 返回的是线程 ID 列表，这个 ID 正是
> watchMem(int, long, int, int, int) 需要的第一个参数。
> 
> 前提：必须先 init(int, int) 连上进程。

- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"threads":[1234,1235,1236]}；未连接时形如 {"ok":false,"error":"尚未连接进程"}
- 版本 : 2.0.3


```javascript
// 拿到线程号之后，才能针对某个线程下监视点
let json = $mem.lsThread();
// 结果形如 {"ok":true,"threads":[1234,1235,1236]}
```


### lsSoInfo(nativeBridge)

> 列出链接器的 soinfo 记录（看隐藏的加载清单）。
> 
> soinfo 是安卓加载器为每一个动态库建立的内部档案，
> 里面能查到在 lsMap(String) 里被隐藏或者改过名字的动态库。
> 
> 前提：必须先 init(int, int) 连上进程。

- 参数 : nativeBridge {boolean} true 列出 NativeBridge（指令集兼容层）的清单；false 列出系统加载器 linker 的清单
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"count":50,"soinfo":[{"pointer":"0x7f0000","base":"0x7f1000","size":8192,"path":"/system/lib64/libc.so"}]}；未连接时形如 {"ok":false,"error":"尚未连接进程"}
- 版本 : 2.0.3


```javascript
// 列出系统加载器的加载清单
let normal = $mem.lsSoInfo(false);
// NativeBridge 用于兼容别的指令集，这种情况上传 true
let bridge = $mem.lsSoInfo(true);
// 结果形如 {"ok":true,"count":50,"soinfo":[{"pointer":"0x7f0000","base":"0x7f1000","size":8192,"path":"/system/lib64/libc.so"}]}
```


### watchMem(threadId, address, type, length, timeoutMs)

> 监视内存访问（硬件断点，找出谁改了这里）。
> 
> 借用 CPU 的性能监控单元盯住某个地址，一旦有人读它或者写它，就会记录一条样本，
> 非常适合排查“不知道被谁改掉了”的问题。
> 
> 注意：这个功能依赖设备内核开放 perf 事件，部分设备用不了；
> 另外这里用的是线程号（TID），不是进程号，请先用 lsThread() 取。

- 参数 : threadId {int} 线程号，取自 lsThread() 的结果，必须大于 0
- 参数 : address {long} 要盯住的地址，必须大于 0；建议做页对齐后使用
- 参数 : type {int} 监视类型：1 只读、2 只写、3 读或写、4 执行；必须落在 1 到 4 之间
- 参数 : length {int} 监视的字节长度，范围 1 到 8
- 参数 : timeoutMs {int} 最长等待时间，单位毫秒，超过 10000 会按 10000 毫秒处理
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"samples":[{"ip":"0x7f1111","address":"0x7f00000000","pid":1234,"tid":1235,"time":123456}]}；失败形如 {"ok":false,"error":"watchpoint 参数无效"} 或 {"ok":false,"error":"硬件 watchpoint 创建失败"}
- 版本 : 2.0.3


```javascript
// type 填 3 表示同时监视读和写，盯 3 秒，最多等 3000 毫秒
let json = $mem.watchMem(1235, 0x7f00000000L, 3, 4, 3000);
// 结果形如 {"ok":true,"samples":[{"ip":"0x7f1111","address":"0x7f00000000","pid":1234,"tid":1235,"time":123456}]}
```


### decodeArmCmd(instruction, address, arm64)

> 反汇编一条 ARM 指令（看机器码到底什么意思）。
> 
> 把 4 个字节的指令字翻译成人能读懂的汇编语句，
> 只翻译你传进来的这四个字节，不会去读目标进程的内存。
> 所以这个方法不需要先连接进程。

- 参数 : instruction {int} 4 个字节的指令机器码，例如 0xd2800001
- 参数 : address {long} 这条指令所在的地址，只影响显示出来的跳转目标和相对地址
- 参数 : arm64 {boolean} true 按 64 位 ARM 解析；false 按 32 位 ARM 解析
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"instruction":"mov x1, #0x1"}
- 版本 : 2.0.3


```javascript
// 翻译一条 64 位 ARM 指令，第三个参数 true 表示按 arm64 处理
let json = $mem.decodeArmCmd(0xd2800001, 0x7f00000000L, true);
// 结果形如 {"ok":true,"instruction":"mov x1, #0x1"}
```


### checkPointer(address, length)

> 检查地址的读写执行权限（动手之前的保险丝）。
> 
> 查询一段地址当前是否可读、可写、可执行，
> 在写入、打补丁之前先查一次，能避免大量把目标进程搞崩的情况。
> 
> 前提：必须先 init(int, int) 连上进程。
> 注意：结果只代表“检查的那一刻”，内存权限随时可能被目标自己改掉。

- 参数 : address {long} 要检查的起始地址
- 参数 : length {int} 要检查的字节长度
- 返回 : {string} JSON 字符串，成功形如 {"ok":true,"readable":true,"writable":false,"executable":true}；未连接时形如 {"ok":false,"error":"尚未连接进程"}
- 版本 : 2.0.3


```javascript
// 确认这块地址能不能写，再决定要不要打补丁
let json = $mem.checkPointer(0x7f00000000L, 8);
// 结果形如 {"ok":true,"readable":true,"writable":false,"executable":true}
```


