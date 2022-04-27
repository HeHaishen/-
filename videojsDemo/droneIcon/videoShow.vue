<!--
 * @Description: 查看无人机视频
 * @Version: 1.0
 * @Autor: hehaishen
 * @LastEditors: hehaishen
 * @Date: 2021-11-16 11:53:27
 * @LastEditTime: 2021-11-25 11:55:17
-->
<template>
  <div>
    <pop-up-layer
      :show="listShow"
      :setStyles="{ zIndex: 9999 }"
      @doClose="listClose"
      title="无人机列表"
      ref="myPopUpLayer"
    >
      <template slot="content">
        <div class="drone-video">
          <ul class="drone-video-ul" :class="[`video-ul-${list.length}`]">
            <li class="video-li" v-for="(i, k) in list" :key="k" :index="i.sid">
              <video
                v-if="
                  i.toLink && i.toLink === 'loadingEndSuccess' && i.pullHttp
                "
                src=""
                class="test-play-flv"
                :index="i.sid"
                :class="`drone-play-video-${i.sid}`"
                controlslist="nodownload noremoteplayback"
                controls
              ></video>
              <p class="video-name-text">{{ i.name }}</p>
              <p
                v-if="i.toLink === 'loadingEndError'"
                class="video-name-text"
                style="color: red; top: 45%"
              >
                {{ "无法链接" }}
              </p>
              <p
                class="c-loading"
                v-if="i.toLink === 'loading' || !i.toLink"
              ></p>
            </li>
          </ul>
        </div>
      </template>
    </pop-up-layer>
  </div>
</template>

<script>
import flvjs from "flv.js";
export default {
  data() {
    return {
      parentdatas: {},
      listShow: false,
      list: [
        /*  {
          deviceId: "91A9597ED0E630D6",
          latitude: 23.07144702727179,
          longitude: 113.38437457892535,
          name: "P1",
          pullHttp: "http://112.94.68.148:8000/live/91A9597ED0E630D6.flv",
          rownum: "1",
          sid: "1459088433594122240",
          state: -1,
          unitName: "广州应急管理局",
        },
        {
          deviceId: "91A9597ED0E630D6",
          latitude: 23.07144702727179,
          longitude: 113.38437457892535,
          name: "P1",
          pullHttp: "http://112.94.68.148:8000/live/91A9597ED0E630D6.flv",
          rownum: "1",
          sid: "1459088433594122240",
          state: -1,
          unitName: "广州应急管理局",
        },
        {
          deviceId: "91A9597ED0E630D6",
          latitude: 23.07144702727179,
          longitude: 113.38437457892535,
          name: "P1",
          pullHttp: "http://112.94.68.148:8000/live/91A9597ED0E630D6.flv",
          rownum: "1",
          sid: "1459088433594122240",
          state: -1,
          unitName: "广州应急管理局",
        }, */
      ],
      videoPlayerArr: [],
    };
  },
  mounted() {
    this.$on("show", (datas) => {
      if (this.videoPlayerArr.length) {
        this.cutVideoPlayerChange();
      }
      this.parentdatas = datas;
      this.list = datas.listDatas;
      this.listShow = true;
      this.$nextTick(() => {
        this.initData();
      });
    });
  },
  methods: {
    initData() {
      this.listShow = true;
      // this.videoPlayerArr = this.list
      this.initPlayerVideos(this.list);
    },
    initPlayerVideos(arr) {
      arr.forEach((i, k) => {
        let videoPlayerDom = document.getElementsByClassName(
          `drone-play-video-${i.sid}`
        )[0];
        let playerVideo = flvjs.createPlayer(
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
      });
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
    listClose() {
      this.cutVideoPlayerChange();
      this.listShow = false;
    },
  },
  beforeDestroy() {
    if (this.videoPlayerArr && this.videoPlayerArr.length) {
      this.cutVideoPlayerChange();
    }
  },
};
</script>

<style lang="less" scoped>
@import "../common.less";
.drone-video {
  width: 1000vw * @w;
  height: 900vh * @h;
  padding: 20vh * @h 20vw * @w;
  .drone-video-ul {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-wrap: wrap;
    li {
      background: black;
      position: relative;
      video {
        display: block;
        width: 100%;
        height: 100%;
      }
      .video-name-text {
        width: 100%;
        height: 40vh * @h;
        font-size: 28vh * @h;
        line-height: 40vh * @h;
        color: white;
        text-align: center;
        position: absolute;
        left: 0;
        top: 0;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
        background: rgba(113, 210, 248, 0.6);
      }
    }
  }
  .video-ul-1 {
    li {
      width: 100%;
      height: 100%;
    }
  }
  .video-ul-2 {
    li {
      width: 48%;
      height: 100%;
    }
  }
  .video-ul-3 {
    li {
      width: 48%;
      height: 48%;
    }
  }
  .video-ul-4 {
    li {
      width: 48%;
      height: 48%;
    }
  }
}
</style>
