<!--
 * @Author: hehaishen
 * @Date: 2022-04-27 11:09:15
 * @LastEditTime: 2022-04-27 14:36:02
 * @LastEditors: Please set LastEditors
 * @Description: 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
 * @FilePath: \ucap-fy-appe:\何海深学习发送文件\easyplayer视频使用文档总结\easyWasmPlayer.md
-->
### video.js 使用方法 总结
---
#### 说明
1) 使用环境说明
~~~~ 在大屏中使用请
 环境说明
  使用的是是基于vue 2 ,vue-cli3环境下使用
  "video.js" 版本：7.18.1
  详细说明可以到一下网址
  https://www.npmjs.com/package/@easydarwin/easywasmplayer
  1、使用方法：
    npm install video.js
  2、Vue-Cli3.0 环境下
    import 'video.js/dist/video-js.css'
    import video_zhCN from 'video.js/dist/lang/zh-CN.json' //引入汉化 中文提示
    import video_en from  'video.js/dist/lang/en.json'
    Video.addLanguage('zh-CN', video_zhCN)
    Video.addLanguage('en', video_en)
    Vue.prototype.$video = Video
  3、vue页面中使用
    <template>
    <div class="box">
        <video class="test-play-flv"></video>
    </div>
    </template>
    <script>
    export default {
        data() {
            return {
            player: '',
            url: 'http://127.0.0.1:10080/fvod/PnCsnxdMg/video.m3u8'
            },
            videoPlayerArr: [],
        },
        mounted() {
            let videoPlayerDom = document.getElementsByClassName(
          `test-play-flv`
        )[0];
        let playerVideo = this.$video.createPlayer(
          {
            type: "flv",
            url: i.pullHttp,
            isLive: true, //直播流
          },
          {
            cors: true,
            isLive: true,
            autoCleanupSourceBuffer: true, //自动清理缓存
            enableStashBuffer: false,
          }
        );
        playerVideo.attachMediaElement(videoPlayerDom);
        playerVideo.load();
        playerVideo.play();
        this.videoPlayerArr.push(playerVideo);
        },
        methods: {
            callbackfun(e) {
                console.log('callbackfun', e);
            },
             // 销毁断流
            cutVideoPlayerChange() {
                let counter = 0;
                this.videoPlayerArr.forEach((player) => {
                    player.pause();

                    player.unload();

                    player.detachMediaElement();

                    player.destroy();

                    player = null;
                    counter = counter + 1;
                    if (counter === this.videoPlayerArr.length) {
                    this.videoPlayerArr = [];
                    }
                });
            },
        },
        destroyed(){
            this.cutVideoPlayerChange()
        }
         
    }
~~~~

2)在使用过程中遇到的问题
~~~~ 基于video.js 7.18.1
1、视频断开后无法重新链接，需要手动进行优化，丢帧时间过程，误会进行跳帧，尚需要优化
2、支持264\不支持265
3、支持265需要使用videojs-flvh265 https://www.jianshu.com/p/33f4c0c5c6ce

