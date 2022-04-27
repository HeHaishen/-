<!--
 *  ┌─────────────────────────────────────────────────────────────┐
 *  │┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐│
 *  ││Esc│!1 │@2 │#3 │$4 │%5 │^6 │&7 │*8 │(9 │)0 │_- │+= │|\ │`~ ││
 *  │├───┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴───┤│
 *  ││ Tab │ Q │ W │ E │ R │ T │ Y │ U │ I │ O │ P │{[ │}] │ BS  ││
 *  │├─────┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴─────┤│
 *  ││ Ctrl │ A │ S │ D │ F │ G │ H │ J │ K │ L │: ;│" '│ Enter  ││
 *  │├──────┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴────┬───┤│
 *  ││ Shift  │ Z │ X │ C │ V │ B │ N │ M │< ,│> .│? /│Shift │Fn ││
 *  │└─────┬──┴┬──┴──┬┴───┴───┴───┴───┴───┴──┬┴───┴┬──┴┬─────┴───┘│
 *  │      │Fn │ Alt │         Space         │ Alt │Win│   HHKB   │
 *  │      └───┴─────┴───────────────────────┴─────┴───┘          │
 *  └─────────────────────────────────────────────────────────────┘
 -->

<!--
 * @Description: 
 * @Version: 1.0
 * @Autor: hehaishen
 * @LastEditors: Please set LastEditors
 * @Date: 2021-10-10 15:34:21
 * @LastEditTime: 2022-04-25 14:46:36
-->
<template>
  <div>
    <ModelBox :title="title" class="c-mybox-position" style="z-index: 8100">
      <template slot="content">
        <div class="around-video-content">
          <ul>
            <li class="video-li" v-for="(i, k) in list" :key="k" :index="i.id">
              <!-- <video
                v-if="
                  i.toLink && i.toLink === 'loadingEndSuccess' && i.playUrlMap
                "
                src=""
                :index="i.id"
                :class="`gj-play-video-${i.id}`"
                controlslist="nodownload noremoteplayback"
                controls
              ></video> -->
              <!-- i['playUrlMap'].flv -->
              <!--   v-if="
                 i.toLink && i.toLink === 'loadingEndSuccess' && i.playUrlMap
                " -->
              <easy-player
                 v-if="
                 i.toLink && i.toLink === 'loadingEndSuccess' && i.playUrlMap
                "
                :id="`gj-play-video-${i.id}`"
                :ref="`gj-play-video-${i.id}`"
                :autoplay="true"
                :video-url="i['playUrlMap'].FLV"
                fluent
                live
                stretch
              ></easy-player>
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
          <div class="grounp-name">{{ grounpName }}</div>
          <div class="grounp-name" v-show="false">
            <a-select
              v-if="grounpList.length"
              v-model="selectValue"
              class="c-select"
              placeholder="选择视频分组"
              dropdownClassName="c-drop-list"
              @change="handleChange"
            >
              <a-select-option
                v-for="(item, index) in grounpList"
                :key="item.sid"
                >{{ item.groupName }}</a-select-option
              >
            </a-select>
          </div>
          <div class="rightTitle">
            <div class="more" @click="onMore">更多</div>
          </div>
          <div class="show-video-wall">
            <a-icon type="left-circle" @click="openVideoWall($event)" />
          </div>
        </div>
      </template>
    </ModelBox>
    <WallVideo
      class="small-video-grounp"
      v-model="wallVideoShow"
      title="视频分组"
      :propEvent="clickSendEvent"
      ref="WallVideoModel"
      setOpsition="bottonLeft"
      @doClose="clickCloseWallModel"
    />
  </div>
</template>

<script>
import ModelBox from "@/views/majorFestivalsConductor/components/modelBox/index.vue";
import flvjs from "flv.js";
import WallVideo from "@/components/APicture/wallVideo/wallVideoindex";
import {
  getGrounpList,
  getGrounpOneVideoList,
  beginVideoStream,
  videoStreamActive,
  stopVideoStream,
} from "@/api/common";
export default {
  components: { ModelBox, WallVideo },
  data() {
    return {
      title: "视频监控",
      emergencyEventCharts: null,
      // 视频分组
      grounpList: [],
      list: [],
      total: 0,
      currentPage: 1,
      saveCanPlayerList: [],
      videoPlayerArr: [], // 播放得视频playerVideo
      timeOuts: null,
      grounpName: "",
      //  视频墙
      wallVideoShow: false,
      clickSendEvent: null,
      selectValue: null,
      selectObj: {},
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.doGetGrounpList({ pageSize: 10, page: 1, body: {} });
      // this.initDatas();
    });
  },
  methods: {
    // 获取分组根节点名称23
    doGetGrounpList(sendObj) {
      let sendData = { ...sendObj };
      getGrounpList({ ...sendData }).then((res) => {
        if (res.success) {
          if (res.body && res.body.length) {
            this.grounpList = res.body;
            this.total = parseInt(res.total);
            this.selectValue = JSON.parse(
              JSON.stringify(this.grounpList[0].sid)
            );
            this.grounpName = this.grounpList[0].groupName;
            this.initDatas(this.grounpList[0]);
          } else {
            this.grounpList = [];
            this.total = 0;
            this.currentPage = 1;
          }
        } else {
          this.total = 0;
          this.currentPage = 1;
          this.$MyMessae.warning("无法查询相关节点");
        }
      });
    },
    initDatas(datas) {
      this.list = [];
      this.total = 0;
      this.currentPage = 1;
      this.doGetGrounpOneVideoList({
        body: { sid: datas.sid ? datas.sid : "" },
        page: this.currentPage,
        pageSize: "4",
      });
    },
    // 接口获取分组下的视频列表
    doGetGrounpOneVideoList(obj) {
      if (this.timeOuts) {
        clearTimeout(this.timeOuts);
      }
      this.saveCanPlayerList = [];
      getGrounpOneVideoList({ ...obj })
        .then(async (res) => {
          if (res.success) {
            if (res.body && res.body.length) {
              // this.list = res.body;
              this.total = parseInt(res.total);
              let sendList = [];
              let saveMap = res.body.map((i, k) => {
                res.body[k].toLink = "loading";
                let { deviceId, id, name } = i;
                sendList.push({
                  deviceId,
                  id,
                  name,
                  toLink: "loading",
                  // loadding-获取了列表，为获取flv，
                  // loadingEndSuccess-获取flv完成并成功、
                  // loadingEndError-获取flv完成并失败;
                });
              });
              let lastRun = await saveMap;
              console.log("sendList", sendList);
              this.list = res.body;

              this.getFLVPlayAddress(sendList, res.body);
            }
            console.log("点击分组视频列表", res);
          } else {
            this.$MyMessage.success("无相关视频墙！");
          }
        })
        .catch((err) => {
          if (err) {
            this.$MyMessage.error("获取分组下的视频列表，失败！");
          }
        });
    },
    // 获取flv 播放地址
    getFLVPlayAddress(arr, showList = []) {
      beginVideoStream(arr)
        .then(async (res) => {
          if (res.success) {
            console.log("获取flv 播放地址", res);
            if (res.body && res.body.length) {
              let sendList = []; // 正确播放的列表-用于保活
              let saveMap = this.list.map((i, k) => {
                let currentObj = null;
                currentObj = res.body.find((fi, fk) => {
                  if (fi.id === i.id) {
                    return fi;
                  }
                });
                if (currentObj) {
                  this.list[k]["playUrlMap"] = currentObj.playUrlMap;
                  this.list[k]["success"] = currentObj.success;
                  if (currentObj.success) {
                    sendList.push(this.list[k]);
                    this.list[k]["toLink"] = "loadingEndSuccess";
                  } else {
                    this.list[k]["toLink"] = "loadingEndError";
                  }
                }
              });
              let lastRun = await saveMap;
              sendList.length && this.doVideoActiveList(sendList)
              this.list = JSON.parse(JSON.stringify(this.list));
              console.log("listssssssss", this.list, sendList.length);
              if (sendList.length) {
                this.saveCanPlayerList = sendList;
                // 播放是视频 #TODO
                // this.initPlayerVideos(sendList);
                /*  this.$nextTick(() => {
                  this.$refs.myplayer.map((pi, pk) => {
                    this.$refs.myplayer[pk].setAttribute(
                      "videoUrl",
                      "https://live.hkstv.hk.lxdns.com/flv/hks.flv"
                    );
                  });
                }); */
                // 处理获取正确的flv保活
                // this.doVideoActiveList(sendList);
              } else {
                this.$MyMessage.error("无可播放地址");
              }
            }
          } else {
            this.$MyMessage.error("获取flv 播放地址，失败！");
          }
        })
        .catch((err) => {
          if (err) {
            this.$MyMessage.error("获取flv 播放地址，失败！");
          }
        });
    },
    // 初始化播放放器并播放
    initPlayerVideos(arr) {
      let that = this;
      arr.forEach((i, k) => {
        let videoPlayerDom = document.getElementById(`gj-play-video-${i.id}`);
        console.log("refsss", that.$refs[`gj-play-video-${i.id}`]);
        videoPlayerDom.setAttribute("video-url", i.playUrlMap.FLV);
        console.log("视频播放》》》", k, videoPlayerDom);
        /*  let videoPlayerDom = document.getElementsByClassName(
          `gj-play-video-${i.id}`
        )[0]; */
        /* let playerVideo = flvjs.createPlayer(
          {
            type: "flv",
            url: i.playUrlMap.FLV,
            isLive: true, //直播流
          },
          {
            cors: true,
            isLive: true,
            autoCleanupSourceBuffer: true, //自动清理缓存
          }
        );
        playerVideo.attachMediaElement(videoPlayerDom);
        playerVideo.load();
        playerVideo.play();
        this.videoPlayerArr.push(playerVideo); */
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
    // 保活接口处理
    doVideoActiveList(arr) {
      videoStreamActive(arr)
        .then((res) => {
          if (res.success) {
            if (this.timeOuts) {
              clearTimeout(this.timeOuts);
            }
            this.timeOuts = setTimeout(() => {
              this.doVideoActiveList(arr);
            }, 10000);
          } else {
            this.$MyMessage.error(
              res.message + ",可能视频会中断，请刷新重试！"
            );
          }
        })
        .catch((error) => {
          if (error) {
            this.$MyMessage.error("可能视频会中断，请刷新重试！");
          }
        });
    },
    //  关闭此页-需要触发得事件
    doCloseThing() {
      if (this.timeOuts) {
        clearTimeout(this.timeOuts);
      }
      if (this.videoPlayerArr.length) {
        this.cutVideoPlayerChange();
        this.doStopVideoStream(this.saveCanPlayerList);
      }
    },
    // 停止流播放
    doStopVideoStream(arr) {
      if (this.timeOuts) {
        clearTimeout(this.timeOuts);
      }
      if (this.saveCanPlayerList.lengt) {
        stopVideoStream(arr)
          .then((res) => {
            if (res.success) {
              this.saveCanPlayerList = [];
            }
          })
          .catch((err) => {
            this.$MyMessage.error("停止播放，失败！");
          });
      }
    },
    // 更多
    onMore() {
      // this.$router.push({ path: "/moreVideos" });
      window.open("#/moreVideos");
    },
    openVideoWall(e) {
      this.clickSendEvent = e; // 如果指定位置-为必传
      this.wallVideoShow = true;
    },
    clickCloseWallModel() {
      this.clickSendEvent = null; // 如果指定位置-为必传
      this.wallVideoShow = false;
    },
    // 切换视频分组
    handleChange(value) {
      if (this.videoPlayerArr.length) {
        this.cutVideoPlayerChange();
        this.doStopVideoStream(this.saveCanPlayerList);
      }
      this.selectObj = this.grounpList.find((i, k) => {
        if (i.sid === value) {
          return i;
        }
      });
      this.initDatas(this.parentDatas);
    },
  },
  destroyed() {
    if (this.videoPlayerArr.length) {
      this.cutVideoPlayerChange();
      this.doStopVideoStream(this.saveCanPlayerList);
    }
    if (this.timeOuts) {
      clearTimeout(this.timeOuts);
    }
  },
};
</script>

<style lang="less" scoped>
@import "./index.less";
</style>
