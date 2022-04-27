<!--
 * @Author: hehaishen
 * @Date: 2022-04-27 11:09:15
 * @LastEditTime: 2022-04-27 14:46:10
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
  https://github.com/tsingsee/EasyPlayer.js
  1、使用方法：
     npm install @easydarwin/easyplayer --save
  2、Vue-Cli3.0 环境下
    copy EasyPlayer-element.min.js 到项目public目录下
    copy EasyPlayer.wasm 到项目public目录下
    使用ng部署的时候记得把文件放在ng跟目录下
  3、vue页面中使用
    <template>
    <div class="box">
       <easy-player
                :id="`gj-play-video-${i.id}`"
                :ref="`gj-play-video-${i.id}`"
                :autoplay="true"
                :video-url="i['playUrlMap'].FLV"
                fluent
                live
                stretch
              ></easy-player>
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
            // 只有获取id 生效
            let videoDiv = document.getElementById(`gj-play-video-${i.id}`)
            videoDiv.setAttribute('video-url',http:aaa.flv)
           
        },
        methods: {
            callbackfun(e) {    
                
            },
            //  销毁
            destroyHandle(){
              
            }
        }
         
    }
~~~~

2)在使用过程中遇到的问题
~~~~ 基于easyplayer 4.0.13



