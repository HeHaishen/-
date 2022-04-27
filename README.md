<!--
 * @Author: hehaishen
 * @Date: 2022-04-27 14:48:18
 * @LastEditTime: 2022-04-27 15:11:19
 * @LastEditors: Please set LastEditors
 * @Description: 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
 * @FilePath: \ucap-fy-appe:\何海深学习发送文件\easyplayer视频使用文档总结\README.md
-->
### 主要用于记录在vue 项目中遇到h265、264视频编码中只用的过程
----------------------------------------------------------------
#### 使用过程
-------
在项目中最先使用的是video.js，由于没有优化，导致视频无法拉去视频流时，直接无法链接，不会继续重试，播放过程中丢帧也不会进行跳帧到时使用体验较差。

--------
后使用easyWasmPlay.js,使用这个播放js,对于跳帧，丢帧，重连都有优化，比较好的支持264播放；
后续使用中突然，视频平台把264直接升级成265，出现了黑屏但是正常拉流，报错c is not a function 报错。

-------
后使用easyplay.js,按照官方提供的demo 中，踩坑过程中，部署时必须把EasyPlayer-element.min、EasyPlayer.wasm放在根目录中，如果修改里面EasyPlayer-element引入EasyPlayer.wasm引入路径，最好是http,否则出现正常拉流，无报错，但是无法播放画面

### 264在线测试视频地址（flv,m3u8,rtsp）
flv
```
http://img.ksbbs.com/asset/Mon_1704/15868902d399b87.flv
http://1011.hlsplay.aodianyun.com/demo/game.flv
```
m3u8
```
http://ivi.bupt.edu.cn/hls/cctv2hd.m3u8
```
rtsp
```
rtsp://wowzaec2demo.streamlock.net/vod/mp4:BigBuckBunny_115k.mov
```
### 如果想了解或学习惯于视频265的封装和原理可以参考这个博主的文章

https://blog.csdn.net/kaimo313/article/details/117090431# userVideoEasypery
