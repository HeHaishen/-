<!--
 * @Author: hehaishen
 * @Date: 2022-04-27 11:09:15
 * @LastEditTime: 2022-04-27 11:40:40
 * @LastEditors: Please set LastEditors
 * @Description: 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
 * @FilePath: \ucap-fy-appe:\何海深学习发送文件\easyplayer视频使用文档总结\easyWasmPlayer.md
-->
### EasyWasmPlay.js 使用方法 总结
---
#### 说明
1) 使用环境说明
~~~~ 在大屏中使用请
 环境说明
  使用的是是基于vue 2 ,vue-cli3环境下使用
  easywasmplayer 版本：4.0.13
  详细说明可以到一下网址
  https://www.npmjs.com/package/@easydarwin/easywasmplayer
  1、使用方法：
    npm install @easydarwin/easywasmplayer --save
  2、Vue-Cli3.0 环境下
    copy node_modules/@easydarwin/easywasmplayer/EasyWasmPlayer.js 到项目public目录下
    copy node_modules/@easydarwin/easywasmplayer/libDecoder.wasm 到项目public目录下
  3、vue页面中使用
    <template>
    <div class="box">
        <div id="Player"></div>
    </div>
    </template>
    <script>
    export default {
        data() {
            return {
            player: '',
            url: 'http://127.0.0.1:10080/fvod/PnCsnxdMg/video.m3u8'
            }
        },
        mounted() {
            // 实例化播放器
            this.player = new WasmPlayer(null, 'Player', this.callbackfun)
            // 调用播放
            this.player.play(this.url, 1)
        },
        methods: {
            callbackfun(e) {
                console.log('callbackfun', e);
            },
            //  销毁
            destroyHandle(){
                this.player.pause();
                this.player.destroy();
                this.player = null;
            }
        },
        destroyed(){
            this.destroyHandle()
        }
         
    }
~~~~

2)在使用过程中遇到的问题
~~~~ 基于easywasmplayer 4.0.13
1、264使用正常不支持265解码，会出现播放器黑屏，并在 浏览器log 中报错：c + function unfinded
2、厂家解释这个文件不再维护，并建议使用easyplayer.js



