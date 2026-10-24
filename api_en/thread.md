# $thread - 并发编程

- 更新时间:2026-10-22 10:55:51

> 多线程（并发）工具对象（脚本里的全局对象 $thread）。
> 
> 脚本默认是“一条路走到底”的：一行行往下执行，碰到耗时操作（比如等待、循环、截图识别）时会卡住。
> $thread 让你能再开几条“后台小路”同时干活：
> <ul>
>     <li>run / 运行：直接在后台启动一个任务（创建并立刻开始）；</li>
>     <li>create / 创建：先造好一个线程对象，需要时再手动 start 启动；</li>
>     <li>loop / 循环：创建一个“每隔一会儿自动跑一次”的循环器；</li>
>     <li>ui / 界面：切回界面主线程去操作界面控件；</li>
>     <li>has / get / stop / stopAll 等：管理这些线程的查询与停止。</li>
> </ul>
> 新手记住：后台任务里要“边做事边睡一会儿”，用全局 sleep(毫秒) 停顿，否则会一直占满 CPU。



```javascript
//在后台开一条线程跑一个耗时任务，不阻塞主线程
$thread.run(function() {
    log("后台任务开始");
    sleep(1000);                 //在后台睡 1 秒
    log("后台任务结束");
});
log("主线程不会被卡住，继续往下走");
```




### ui(runnable)

> 切到“界面主线程”里执行一段代码。
> 
> 安卓规定：只有界面主线程才能操作界面上的控件（比如改文字、弹提示）。
> 如果你在后台线程里想更新界面，就把这段代码包进 function 传给 ui，它会被丢到主线程去跑。
> 本方法没有返回值，传进去的 function 会被异步执行。
> 输出：void，表示没有返回数据；不要把调用结果当作成功标志。

- 参数 : runnable {function} 要在界面主线程里执行的代码，写成 function() { ... }
- 版本 : 1.0.0


```javascript
//先在后台线程里干活
$thread.run(function() {
    sleep(1000);                       //后台模拟耗时 1 秒
    //干完了，切回主线程去操作界面
    $thread.ui(function() {
        log("现在运行在界面主线程里，可以安全操作界面控件");
    });
});
```


### run(runnable)

> 在后台创建并立刻启动一个线程（最常用的“开后台任务”写法）。
> 
> 你把要在后台跑的代码写成 function 传进来，方法会自动创建线程并马上开始运行。
> 返回这个线程对象（Threadx），后面想中途停掉它，就用这个对象调用它的停止方法。
> 主线程不会等待它跑完，会继续往下走。

- 参数 : runnable {function} 要在后台执行的任务，写成 function() { ... }
- 返回 : {Threadx} 刚启动的后台线程对象，可用来停止或查询状态
- 版本 : 1.2.0


```javascript
//启动一个后台线程，并拿到线程对象，方便以后停止
var t1 = $thread.run(function() {
    //这里是后台的耗时任务
    for (var i = 0; i < 5; i++) {
        sleep(500);                 //每次循环睡半秒
        log("后台第 " + i + " 次");
    }
});
//以后想提前停止它，就调用线程对象的停止方法
t1.kill();
```


### create(runnable)

> 创建一个后台线程（只创建、不自动启动）。
> 
> 和 run 的区别：create 只是“把线程准备好”，并不会立刻跑，需要你后面手动调用线程对象的 start() 才开始。
> 它会自动给线程起一个名字并存起来，方便之后用名字 get / stop。
> 适合“先把任务都准备好，挑个时间再统一启动”的场景。

- 参数 : runnable {function} 这个线程要执行的任务，写成 function() { ... }
- 返回 : {Threadx} 创建好的线程对象，需要调用它的 start() 才会真正开始运行
- 版本 : 1.0.0


```javascript
//第一步：创建一个线程（此时还没开始跑）
var t1 = $thread.create(function() {
    for (var i = 0; i < 10; i++) {
        sleep(300);                       //每 0.3 秒打印一次
        log(t1.getName() + "==>" + i);
    }
    log(t1.getName() + "执行完毕");
});
//第二步：需要的时候手动启动它
t1.start();
```


### create(name, runnable)

> 创建一个带名字的后台线程（只创建、不自动启动）。
> 
> 比 create(任务) 多了一个“线程名字”参数：你可以给线程起个好记的名字，
> 之后就能用这个名字通过 get / has / stop 找到或停止它。
> 如果这个名字已经被用过了，方法不会新建，而是直接返回那个同名的旧线程。
> 创建后仍需手动调用线程对象的 start() 才会开始跑。

- 参数 : name {string} 给这个线程起的名字，之后靠它查找/停止；名字重复时会返回旧线程
- 参数 : runnable {function} 这个线程要执行的任务，写成 function() { ... }
- 返回 : {Threadx} 创建好的线程对象，需调用 start() 才会运行
- 版本 : 1.0.0


```javascript
//创建一个叫"下载任务"的线程
var t1 = $thread.create("下载任务", function() {
    for (var i = 0; i < 10; i++) {
        sleep(300);
        log(t1.getName() + "==>" + i);
    }
    log(t1.getName() + "执行完毕");
});
//手动启动
t1.start();
```


### newCdLock(num)

> 新建一个“倒计时锁”（用来等多个后台任务都做完再继续）。
> 
> 倒计时锁像一个计数器：一开始设成 n，每当一个后台任务做完就调一次 ok()，计数器减 1。
> 主线程调用 finish(超时毫秒) 会一直等，直到计数器减到 0 才继续往下走（或超时返回 false）。
> 适合“我开了 3 个子任务，想等它们全部完成后再做下一步”的场景。

- 参数 : num {Number} 初始计数，传非负整数；内部取整数部分，负数会抛出异常，传 null 返回 null
- 返回 : {CdLock} 新建好的倒计时锁对象；传入 null 时返回 null
- 版本 : 1.8.3


```javascript
//建一个计数器为 2 的倒计时锁，表示要等 2 个任务完成
var lock = $thread.newCdLock(2);
//开第一个后台任务
$thread.run(function() {
    sleep(500);          //模拟干活
    lock.ok();           //干完了，计数器减 1
});
//开第二个后台任务
$thread.run(function() {
    sleep(800);          //模拟干活
    lock.ok();           //干完了，计数器减 1
});
//主线程在这里等着，直到两个任务都 ok()，最多等 5 秒
var done = lock.finish(5000);
log("两个任务都完成了吗：" + done);
```


### has(name)

> 判断某个名字的线程是否已经存在。
> 
> 你之前用 create(名字, 任务) 创建过带名字的线程，这里就能用名字查它还在不在登记簿里。
> 返回 true 表示存在，false 表示没有这个名字的线程。

- 参数 : name {string} 要检查的线程名字
- 返回 : {boolean} 存在返回 true，不存在返回 false
- 版本 : 1.2.0


```javascript
//先创建一个带名字的线程
$thread.create("下载任务", function() { sleep(1000); });
//查一下这个名字的线程存不存在
var has = $thread.has("下载任务");
if (has) {
    log("这个线程存在");
} else {
    log("这个线程不存在");
}
```


### get(name)

> 按名字取出一个已经创建好的线程对象。
> 
> 你在别的地方用 create(名字, 任务) 创建过线程后，可以在脚本任意位置用这个名字把它再取回来，
> 然后对它做启动、停止等操作。找不到这个名字时返回 null。

- 参数 : name {string} 要取出的线程名字
- 返回 : {Threadx} 对应的线程对象；没有这个名字时返回 null
- 版本 : 1.0.0


```javascript
//先创建一个带名字的线程
$thread.create("下载任务", function() { sleep(1000); });
//之后在别处按名字把它取出来
var t1 = $thread.get("下载任务");
if (t1 != null) {
    t1.start();        //取到了就启动它
}
```


### loop(name, runnable)

> 创建一个“循环执行器”（让一段代码自动反复跑）。
> 
> 普通线程只跑一次就结束；循环器会把你给的任务一直重复执行，非常适合“每隔 1 秒看一眼屏幕有没有变化”这种常驻监控。
> 它会按名字登记，之后用 hasLoop 查、用 stopLoop 停。
> 注意：本方法只创建，返回的线程对象仍需调用 start() 才会真正开始循环；循环体为空会返回 null，名字重复也会返回 null。

- 参数 : name {string} 给这个循环器起的名字，之后靠它查找/停止
- 参数 : runnable {function} 要反复执行的任务，写成 function() { ... }
- 返回 : {Threadx} 代表这个循环器的线程对象，需调用 start() 启动；名字重复或任务为空时返回 null
- 版本 : 1.0.0


```javascript
//创建一个叫"循环1号"的循环器：每隔 1 秒打印一次
var t1 = $thread.loop("循环1号", function() {
    sleep(1000);                 //每次循环间隔 1 秒
    log("我还活着！");
});
//启动它开始循环
if (t1 != null) { //重名或回调为空时拿不到线程，必须先检查
    t1.start(); //继承的线程启动方法，没有中文别名
}
//以后想停掉这个循环器
// $thread.stopLoop("循环1号");
```


### hasLoop(name)

> 判断某个名字的循环器是否还存在。
> 
> 对应 loop(名字, 任务) 创建出来的循环器。返回 true 表示这个循环器还在，false 表示没有或已被停止。

- 参数 : name {string} 要检查的循环器名字
- 返回 : {boolean} 存在返回 true，不存在返回 false
- 版本 : 1.0.0


```javascript
//先创建一个循环器
$thread.loop("循环1号", function() { sleep(1000); });
//查它还在不在
var exists = $thread.hasLoop("循环1号");
log("这个循环器存在吗：" + exists);
```


### stopLoop(name)

> 停止并关闭一个指定名字的循环器。
> 
> 通知 loop(名字, 任务) 创建的循环器不要开始下一轮，并删除它的登记项；当前这一轮可能尚未结束。
> 名字不存在也不会报错。本方法没有返回值。
> 输出：void，表示没有返回数据；不要把调用结果当作成功标志。

- 参数 : name {string} 要停止的循环器名字
- 版本 : 1.0.0


```javascript
//先创建一个循环器
var t = $thread.loop("循环1号", function() { sleep(1000); });
t.start();
//过一会儿把它停掉
$thread.stopLoop("循环1号");
```


### stop(threadx)

> 停止一个线程（直接传线程对象进去）。
> 
> 把 run / create 返回的那个线程对象传进来，方法会通知它停止、并把它从登记簿里移除。
> 传入 null 什么也不做。本方法没有返回值。
> 输出：void，表示没有返回数据；不要把调用结果当作成功标志。

- 参数 : threadx {Threadx} 要停止的线程对象（用 run/create 得到）；传 null 不做任何事
- 版本 : 1.0.0


```javascript
//先启动一个后台任务，拿到线程对象
var t1 = $thread.run(function() {
    while (true) {
        sleep(500);
        log("还在跑...");
    }
});
//过两秒后停掉它
sleep(2000);
$thread.stop(t1);
```


### stop(threadName)

> 按名字停止一个线程。
> 
> 如果你创建的是带名字的线程（create(名字, 任务)），这里直接传名字就能停掉它，不必再保留线程对象。
> 名字不存在也不会报错。本方法没有返回值。
> 输出：void，表示没有返回数据；不要把调用结果当作成功标志。

- 参数 : threadName {string} 要停止的线程名字
- 版本 : 1.0.0


```javascript
//先创建一个带名字的线程并启动
var t = $thread.create("示例", function() {
    while (true) { sleep(500); }
});
t.start();
//之后按名字停掉它
$thread.stop("示例");
```


### stopAll()

> 对当前登记的所有线程发出停止请求。
> 
> 一键把目前登记簿里所有用 run / create 开出来的后台线程全部停掉。
> 循环器对应的线程也登记在同一张表中，因此同样会收到请求；循环器登记项需要再调用 stopAllLoop 清理。
> 本方法没有返回值。
> 输出：void，表示没有返回数据；不要把调用结果当作成功标志。
> 输入：无参数。

- 版本 : 1.0.0


```javascript
//开了好几个后台线程
$thread.run(function() { while (true) { sleep(500); } });
$thread.run(function() { while (true) { sleep(500); } });
//脚本结束前，一键停掉所有普通后台线程
$thread.stopAll();
```


### stopAllLoop()

> 停止所有循环执行器。
> 
> 一键把目前所有用 loop 创建出来的循环器全部停掉。和 stopAll 互补：
> stopAll 遍历线程登记表；stopAllLoop 遍历循环器登记表并逐个请求停止。本方法没有返回值。
> 输出：void，表示没有返回数据；不要把调用结果当作成功标志。
> 输入：无参数。

- 版本 : 1.0.0


```javascript
//开了一个循环器
var t = $thread.loop("循环1号", function() { sleep(1000); });
t.start();
//脚本结束前，一键停掉所有循环器
$thread.stopAllLoop();
```


