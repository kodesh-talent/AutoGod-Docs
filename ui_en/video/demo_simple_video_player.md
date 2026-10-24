# 案例-简易播放器

- 更新时间:2026-10-22 10:58:42



本示例将展示一个简单的播放器


## Xml代码


```javascript
// 将布局内容作为字符串传入解析方法；返回值是可查找控件的界面对象。
var layout =
    "<ui>\n" +
    "    <statusbar/>\n" +
    "    <linear w=\"max\" h=\"max\" gravity=\"center\">\n" +
    "        <!--视频:当使用约束布局的时候,视频可以被展开,但未必是全屏的\n" +
    "        path:可以指定相对路径,也可以指定绝对路径\n" +
    "        autoStart:当视频加载完成之后，会自动播放视频\n" +
    "        loop:是否循环播放视频\n" +
    "        -->\n" +
    "        <video autoStart=\"true\" id=\"video\" loop=\"true\"\n" +
    "               path=\"video.mp4\" w=\"max\"/>\n" +
    "        <!--跳转到指定的视频位置进行播放-->\n" +
    "        <slider w=\"max\" id=\"slide\" />\n" +
    "        <!--\n" +
    "        播放/暂停\n" +
    "        ic_play_arrow_fill\n" +
    "        ic_pause_outline\n" +
    "        -->\n" +
    "        <button id=\"play\" style=\"icon\" icon=\"ic_pause_outline\" />\n" +
    "    </linear>\n" +
    "</ui>\n";
var ui = $ui.layout(layout);
```


## JS代码


```javascript
var ui = $ui.layout("main.xml");
var mAppbar = ui.id("mAppbar");
if (mAppbar != null) {
    mAppbar.back(function() {
        ui.finish();
    });
}
var video = ui.id("video");
var slide = ui.id("slide");
var play = ui.id("play");
//监听(人手滑动)
slide.onChange(function(val){
    //video 跳转 不准确性
    video.seekTo(val);
});
play.click(function() {
    if (video.isPlaying()) {
        //暂停播放
        video.pause();
        play.setIcon("ic_play_arrow_fill");
    } else {
        //开始播放
        video.start();
        play.setIcon("ic_pause_outline");
    }
});
var intervalId = setInterval(function(){
    if(video.isPlaying()){
        slide.setTo(video.getDur());//最大值 视频的总时长
        slide.setValue(video.getCur());//当前值 视频当前的进度
    }
},10);
ui.onDestroy(function(activity){
    //释放循环器
    clearInterval(intervalId);
});
//最好放在最后显示主界面
ui.show();
```


