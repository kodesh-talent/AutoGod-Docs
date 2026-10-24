# TtsOptions - 语音配置

- 更新时间:2026-10-22 10:55:52

> 语音朗读的配置对象（用来定制 $tts 说话时的语速、音调、音量、语言和出声通道）。
> 
> 这个对象里同时存在两套字段：一套是英文名（rate、pitch、volume、language、streamType），
> 一套是对应的中文名（速度、音调、音量、语言、类型），它们其实是同一个设置，只是写法不同。
> 一般不需要自己 new 它，调用 $tts 的朗读方法时按提示传入即可；自己创建时用下面的示例。



```javascript
//通常更简单的写法：直接传一个配置对象给 $tts.read
$tts.read("你好，世界", {
    rate: 1.0,     //语速
    pitch: 1.0,    //音调
    volume: 1.0,   //音量
    language: "zh",//语言
    streamType: "music"  //出声通道
});
```




### const {Float} 速度;

> 播放倍速


### const {Float} 音调;

> 音调


### const {Float} 音量;

> 音量


### const {String} 语言;

> 语言
> 
> 可选值有：zh,en,fr,de,it,ja,ko
> 
> 分别意思：中文,英文,法文,德文,意大利文,日文,韩文


### const {String} 类型;

> 播放流类型
> 
> 这是上面 streamType 字段的中文写法，作用完全一样：指定朗读声音从哪条声音通道出来。
> 可填的值与 streamType 相同（music、alarm、notification、ring、system、call、dtmf）。
> 同时设置时，中文字段优先。


```javascript
$语音.阅读("我在用通知通道播放", { 类型: "notification" });
```


