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




### newSqlite()

> 新建一个独立的数据库操作对象。
> 
> 平时用 $sqlite 直接操作就行。如果你要同时操作多个互不相干的数据库，
> 可以用这个方法再拿一个对象，各管各的。

- 返回 : {AgSqLite} 一个新的数据库操作对象


```javascript
var sqlite = $sqlite.newSqlite();   //再拿一个数据库对象
var hasOpen = sqlite.open("myDb");   //用它打开另一个库
if (hasOpen) {
    log("连接成功");
}
```


### open(dbName, external)

> 打开（没有就创建）一个数据库，可以指定存在内部还是外部存储。
> 
> 第二个参数 external：
> <ul>
>   <li>false：存在应用内部存储，只要给个库名（不用后缀），应用卸载后数据会被删；</li>
>   <li>true：存在外部存储，要给完整路径（含文件名和 .db 后缀），卸载后数据还在。</li>
> </ul>
> 返回 true 表示打开成功。

- 参数 : dbName {String} 库名（内部存储只要名字；外部存储要完整路径）
- 参数 : external {boolean} true 存外部存储，false 存内部存储
- 返回 : {boolean} true 表示打开成功


```javascript
//打开外部存储里的一个数据库（给完整路径）
var hasOpen = $sqlite.open("/sdcard/mData.db", true);
if (hasOpen) {
    log("连接成功");
}
```


### open(dbName)

> 打开（没有就创建）一个数据库，默认存在应用内部存储。
> 
> 只要给一个库名即可（不用写 .db 后缀）。应用卸载后数据会被删除。
> 返回 true 表示打开成功。

- 参数 : dbName {String} 数据库名称（不用后缀）
- 返回 : {boolean} true 表示打开成功


```javascript
var hasOpen = $sqlite.open("VideoData");   //只要给个库名
if (hasOpen) {
    log("连接成功");
}
```


### newTab(tableName, columns)

> 新建一张数据表（如果已存在则不重复创建）。
> 
> 第一个参数是表名，第二个参数是列名数组。系统会自动加一个自增 id 作为主键。
> 注意：不管你以后存什么类型，列都按字符串类型存。
> 调用前要先 open 打开数据库。返回 true 表示建表成功。

- 参数 : tableName {String} 表名
- 参数 : columns {Collection} 列名列表
- 返回 : {boolean} true 表示建表成功


```javascript
$sqlite.open("demo.db");
//建一张表，有 name、sex、age 三列（id 列自动加）
var hasTable = $sqlite.newTab("table1", ["name", "sex", "age"]);
if (hasTable) {
    log("建表成功");
}
```


### add(tableName, data)

> 往表里加一行数据。
> 
> 第二个参数是一个对象，{列名: 值} 的形式，列要和建表时一致。
> 默认用自增 id 作为主键，数据都按字符串存。返回 true 表示添加成功。

- 参数 : tableName {String} 表名
- 参数 : data {Map} 一行数据，{列名: 值}
- 返回 : {boolean} true 表示添加成功


```javascript
$sqlite.open("demo.db");
$sqlite.newTab("table1", ["name", "sex", "age"]);
//加一行：name=张三、sex=男、age=20
var hasAdd = $sqlite.add("table1", {name: "张三", sex: "男", age: 20});
if (hasAdd) {
    log("添加成功");
}
```


### update(tableName, map, where)

> 更新表里满足条件的那些行。
> 
> 第二个参数是要改成的新值 {列名: 新值}；第三个参数是“条件”，
> 例如 "name='张三'" 表示只改 name 为张三的行。返回 true 表示成功。

- 参数 : tableName {String} 表名
- 参数 : map {Map} 要改成的新值 {列名: 新值}
- 参数 : where {String} 条件语句，例如 "name='张三'"
- 返回 : {boolean} true 表示更新成功


```javascript
$sqlite.open("demo.db");
//把 name 等于“张三”的那行，性别改成女、年龄改成 20
var okUpdate = $sqlite.update("table1", {sex: "女", age: 20}, "name='张三'");
if (okUpdate) {
    log("更新成功");
}
```


### ls(tableName)

> 列出某张表里的全部数据。
> 
> 相当于 select * from 表名。返回一个列表，每一项是一行数据（{列名: 值}）。

- 参数 : tableName {String} 表名
- 返回 : {List} 表里所有行的列表


```javascript
$sqlite.open("demo.db");
var result = $sqlite.ls("table1");
for (var i = 0; i < result.size(); i++) {
    log(result.get(i));   //逐行打印
}
```


### ls()

> 列出当前数据库里所有表的名字。
> 
> 返回一个表名列表，用来看看这个库里都建过哪些表。

- 返回 : {List} 所有表名的列表


```javascript
$sqlite.open("demo.db");
var result = $sqlite.ls();   //列出所有表名
for (var i = 0; i < result.size(); i++) {
    log("第" + i + "张表：" + result.get(i));
}
```


### select(selectSql)

> 执行一条查询 SQL，返回查出来的所有行。
> 
> 参数就是一段 SQL 查询语句，例如 "select * from table1 where age>18"。
> 返回列表里每一项是一行数据（{列名: 值}）。

- 参数 : selectSql {String} 查询 SQL 语句
- 返回 : {List} 查到的所有行


```javascript
$sqlite.open("demo.db");
var result = $sqlite.select("select * from table1");
for (var i = 0; i < result.size(); i++) {
    var row = result.get(i);
    log("第" + i + "行：" + row);
}
```


### hasTab(tableName)

> 判断某张表是否已经存在。
> 
> 返回 true 表示库里有这张表，false 表示没有。

- 参数 : tableName {String} 要判断的表名
- 返回 : {boolean} true 表示存在，false 表示不存在


```javascript
$sqlite.open("demo.db");
var result = $sqlite.hasTab("table1");
if (result) {
    log("存在这张表");
} else {
    log("没有这张表");
}
```


### exe(sql)

> 执行一条不返回结果的 SQL 语句（例如删表、插入、删除、修改）。
> 
> 查询用 select，这种“改库”的语句用 exe。返回 true 表示执行成功。

- 参数 : sql {String} 要执行的 SQL 语句
- 返回 : {boolean} true 表示执行成功


```javascript
$sqlite.open("demo.db");
//删除名为 table1 的表
$sqlite.exe("drop table if exists table1");
log("已执行删表语句");
```


### delDb(external)

> 删除“当前正在操作”的这个数据库文件（数据会全部丢失）。
> 
> 参数 external 传 false 删内部存储的库，传 true 删外部存储的库。
> 这是直接删文件，删完找不回来，谨慎使用。

- 参数 : external {boolean} false 删内部存储的库，true 删外部存储的库
- 返回 : {boolean} true 表示删除完成


```javascript
//删除应用私有目录里的当前数据库
var deleted = $sqlite.delDb(false);
if (deleted) {
    log("删库成功");
}
```


### delDb(dbName, external)

> 按名字删除指定的数据库文件（不用先打开）。
> 
> 第一个参数是库名，第二个参数 false 表示在内部存储找、true 表示在外部存储找。
> 直接删文件，数据找不回来。

- 参数 : dbName {String} 要删除的库名
- 参数 : external {boolean} false 删内部存储，true 删外部存储
- 返回 : {boolean} true 表示删除完成


```javascript
//直接删除名为 VideoData 的数据库，无需先打开
var hasDelDb = $sqlite.delDb("VideoData", false);
if (hasDelDb) {
    log("删库成功");
}
```


### delDb(dbName)

> 按名字删除内部存储里的某个数据库文件（不用先打开）。
> 
> 只给一个库名，默认在内部存储里找并删除。直接删文件，谨慎使用。

- 参数 : dbName {String} 要删除的库名
- 返回 : {boolean} true 表示删除完成


```javascript
//直接删除名为 VideoData 的内部数据库
var hasDelDb = $sqlite.delDb("VideoData");
if (hasDelDb) {
    log("删库成功");
}
```


### delTab(table)

> 删除指定的一张表（连同里面所有数据）。
> 
> 传表名即可，表里的数据会一起删掉。返回 true 表示删除成功。

- 参数 : table {String} 要删除的表名
- 返回 : {boolean} true 表示删除成功


```javascript
$sqlite.open("demo.db");
var hasDel = $sqlite.delTab("table1");
if (hasDel) {
    log("删除表成功");
}
```


### close()

> 关闭数据库连接，释放资源。
> 
> 操作完数据库后调用它，释放占用。返回 true 表示关闭完成。

- 返回 : {boolean} true 表示关闭完成


```javascript
$sqlite.open("demo.db");
//...各种增删改查...
var okFinish = $sqlite.close();
if (okFinish) {
    log("结束操作，已关闭数据库");
}
```


