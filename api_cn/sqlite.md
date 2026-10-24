# $sqlite - 轻量数据库

- 更新时间:2026-10-22 10:55:51

> 轻量数据库（脚本里直接用 $sqlite 或 $小数据库）。
> 
> 它像一个“会长期保存的表格本子”：可以建表、往里加一行行数据、按条件改、查、删。
> 脚本关掉再打开，数据还在。
> 
> 基本流程：
> <ol>
>   <li>open("库名") 打开或创建一个数据库；</li>
>   <li>newTab("表名", [列名1, 列名2]) 建一张表；</li>
>   <li>add("表名", {...}) 加一行数据；</li>
>   <li>select("select * from 表名") 查询；</li>
>   <li>用完 close() 关闭。</li>
> </ol>
> 新手提示：表里的数据不管你传什么类型，都按字符串存。



```javascript
//打开（没有就创建）一个叫 demo 的数据库
var opened = $sqlite.open("demo.db");
if (opened) {
    //建一张表，含 name、sex、age 三列
    $sqlite.newTab("table1", ["name", "sex", "age"]);
    //加一行数据
    $sqlite.add("table1", {name: "张三", sex: "男", age: 20});
    //查出来看看
    var rows = $sqlite.select("select * from table1");
    for (var i = 0; i < rows.size(); i++) {
        log(rows.get(i));
    }
    $sqlite.close();
}
```




### 创建新对象()

> 新建一个独立的数据库操作对象（中文方法名“创建新对象”）。
> 
> 和 newSqlite() 是同一个功能，只是方法名用中文。

- 返回 : {AgSqLite} 一个新的数据库操作对象


```javascript
var sqlite = $sqlite.创建新对象();
var hasOpen = sqlite.打开("我的数据2", false);
if (hasOpen) {
    log("连接成功");
}
```


### 打开(库名称, 是否存于外部存储)

> 打开（没有就创建）一个数据库，可指定内部或外部存储（中文方法名“打开”）。
> 
> 和 open(库名, 是否外部) 是同一个功能。
> 第二个参数：false 存内部（只要库名，卸载后删除）；true 存外部（要完整路径，卸载后保留）。

- 参数 : 库名称 {String} 库名或完整路径
- 参数 : 是否存于外部存储 {boolean} true 外部，false 内部
- 返回 : {boolean} true 表示打开成功


```javascript
var 打开成功 = $sqlite.打开("/sdcard/mData.db", true);
if (打开成功) {
    log("连接成功");
}
```


### 打开(库名称)

> 打开（没有就创建）一个数据库，默认存在内部存储（中文方法名“打开”）。
> 
> 和 open(库名) 是同一个功能，只要给个库名即可。

- 参数 : 库名称 {String} 数据库名称（不用后缀）
- 返回 : {boolean} true 表示打开成功


```javascript
var 打开成功 = $sqlite.打开("我的数据");
if (打开成功) {
    log("连接成功");
}
```


### 创建表(表名, 列名)

> 新建一张数据表（中文方法名“创建表”）。
> 
> 和 newTab() 是同一个功能。不管数据是什么类型都按字符串存，自动加自增 id 主键。

- 参数 : 表名 {String} 表名
- 参数 : 列名 {Collection} 列名列表
- 返回 : {boolean} true 表示建表成功


```javascript
$sqlite.打开("demo.db");
var 创建成功 = $sqlite.创建表("表1", ["姓名", "性别", "年龄"]);
if (创建成功) {
    log("建表成功");
}
```


### 添加(表名, 数据)

> 往表里加一行数据（中文方法名“添加”）。
> 
> 和 add() 是同一个功能。数据都按字符串存，默认用自增 id 作主键。

- 参数 : 表名 {String} 表名
- 参数 : 数据 {Map} 一行数据，{列名: 值}
- 返回 : {boolean} true 表示添加成功


```javascript
$sqlite.打开("demo.db");
$sqlite.创建表("表1", ["姓名", "性别", "年龄"]);
var 添加成功 = $sqlite.添加("表1", {姓名: "张三", 性别: "男", 年龄: 20});
if (添加成功) {
    log("添加成功");
}
```


### 更新(表名, 数据, 条件语句)

> 更新表里满足条件的那些行（中文方法名“更新”）。
> 
> 和 update() 是同一个功能。第三个参数是条件，例如 "姓名='张三'"。

- 参数 : 表名 {String} 表名
- 参数 : 数据 {Map} 要改成的新值 {列名: 新值}
- 参数 : 条件语句 {String} 条件，例如 "姓名='张三'"
- 返回 : {boolean} true 表示更新成功


```javascript
$sqlite.打开("demo.db");
var 更新成功 = $sqlite.更新("表1", {性别: "女", 年龄: 20}, "姓名='张三'");
if (更新成功) {
    log("更新成功");
}
```


### 罗列(表名)

> 列出某张表里的全部数据（中文方法名“罗列”）。
> 
> 和 ls(表名) 是同一个功能。返回每一行数据的列表。

- 参数 : 表名 {String} 表名
- 返回 : {List} 表里所有行的列表


```javascript
$sqlite.打开("demo.db");
var 结果集 = $sqlite.罗列("表1");
for (var i = 0; i < 结果集.size(); i++) {
    log(结果集.get(i));
}
```


### 罗列()

> 列出当前数据库里所有表的名字（中文方法名“罗列”）。
> 
> 和 ls() 是同一个功能。

- 返回 : {List} 所有表名的列表


```javascript
$sqlite.打开("demo.db");
var 结果集 = $sqlite.罗列();
for (var i = 0; i < 结果集.size(); i++) {
    log("第" + i + "张表：" + 结果集.get(i));
}
```


### 查询(sql语句)

> 执行一条查询 SQL，返回查出来的所有行（中文方法名“查询”）。
> 
> 和 select() 是同一个功能。

- 参数 : sql语句 {String} 查询 SQL 语句
- 返回 : {List} 查到的所有行


```javascript
$sqlite.打开("demo.db");
var 结果列表 = $sqlite.查询("select * from table1");
for (var i = 0; i < 结果列表.size(); i++) {
    log(结果列表.get(i));
}
```


### 有表(表名称)

> 判断某张表是否已经存在（中文方法名“有表”）。
> 
> 和 hasTab() 是同一个功能。

- 参数 : 表名称 {String} 要判断的表名
- 返回 : {boolean} true 表示存在，false 表示不存在


```javascript
$sqlite.打开("demo.db");
if ($sqlite.有表("我的表格")) {
    log("存在这张表");
} else {
    log("没有这张表");
}
```


### 执行(sql语句)

> 执行一条不返回结果的 SQL 语句（中文方法名“执行”）。
> 
> 和 exe() 是同一个功能，用于删表、插入、删除、修改等语句。

- 参数 : sql语句 {String} 要执行的 SQL 语句
- 返回 : {boolean} true 表示执行成功


```javascript
$sqlite.打开("demo.db");
$sqlite.执行("drop table if exists table1");
log("已执行删表语句");
```


### 删除数据库(外部数据)

> 删除“当前正在操作”的这个数据库文件（中文方法名“删除数据库”）。
> 
> 和 delDb() 是同一个功能。直接删本地文件，数据会全部丢失，谨慎使用。

- 参数 : 外部数据 {boolean} false 删内部存储的库，true 删外部存储的库
- 返回 : {boolean} true 表示删除完成


```javascript
var 删除成功 = $sqlite.删除数据库(false);
if (删除成功) {
    log("删库成功");
}
```


### 删除数据库(库名, 外部数据)

> 按名字删除指定的数据库文件（中文方法名“删除数据库”）。
> 
> 和 delDb(库名, 是否外部) 是同一个功能，不用先打开。直接删文件，谨慎使用。

- 参数 : 库名 {String} 要删除的库名
- 参数 : 外部数据 {boolean} false 删内部存储，true 删外部存储
- 返回 : {boolean} true 表示删除完成


```javascript
var 删除成功 = $sqlite.删除数据库("我的数据", false);
if (删除成功) {
    log("删库成功");
}
```


### 删除数据库(库名)

> 按名字删除内部存储里的某个数据库文件（中文方法名“删除数据库”）。
> 
> 和 delDb(库名) 是同一个功能，默认删内部存储。

- 参数 : 库名 {String} 要删除的库名
- 返回 : {boolean} true 表示删除完成


```javascript
var 删除成功 = $sqlite.删除数据库("我的数据");
if (删除成功) {
    log("删库成功");
}
```


### 删除表(表名)

> 删除指定的一张表（中文方法名“删除表”）。
> 
> 和 delTab() 是同一个功能，表里数据会一起删掉。

- 参数 : 表名 {String} 要删除的表名
- 返回 : {boolean} true 表示删除成功


```javascript
$sqlite.打开("demo.db");
var 删除成功 = $sqlite.删除表("表1");
if (删除成功) {
    log("删除表成功");
}
```


### 关闭()

> 关闭数据库连接，释放资源（中文方法名“关闭”）。
> 
> 和 close() 是同一个功能。操作完后调用。

- 返回 : {boolean} true 表示关闭完成


```javascript
$sqlite.打开("demo.db");
//...各种增删改查...
var 成功关闭 = $sqlite.关闭();
if (成功关闭) {
    log("结束操作，已关闭数据库");
}
```


