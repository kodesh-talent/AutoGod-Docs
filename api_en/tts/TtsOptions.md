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




### const {float} rate;

> 播放倍速


### const {float} pitch;

> 音调


### const {float} volume;

> 音量


### const {String} language;

> 语言
> 
> 可选值有：zh,en,fr,de,it,ja,ko
> 
> 分别意思：中文,英文,法文,德文,意大利文,日文,韩文


### const {String} streamType;

> 播放流类型
> 
> 指定朗读声音从手机的哪条"声音通道"出来，不同通道对应系统里不同的音量调节开关。
> 写法是字符串，按开头字母匹配即可，常用取值：
> <ul>
>     <li>"music"：媒体音乐通道（默认值），受"媒体音量"控制，最常用；</li>
>     <li>"alarm"：闹钟通道，受"闹钟音量"控制；</li>
>     <li>"notification"：通知提示音通道；</li>
>     <li>"ring"：铃声通道；</li>
>     <li>"system"：系统提示音通道；</li>
>     <li>"call"：通话音量通道；</li>
>     <li>"dtmf"：按键音通道。</li>
> </ul>
> 不传或匹配不上时，默认按 music 媒体通道播放。


```javascript
$tts.read("我在用闹钟通道播放", { streamType: "alarm" });
```


