<!--
 * @Description: 地图工具箱
 * @Version: 1.0
 * @Autor: hehaishen
 * @LastEditors: hehaishen
 * @Date: 2021-10-29 16:52:18
 * @LastEditTime: 2022-01-07 11:17:27
-->
<template>
  <div class="all-icons-box drone-icon">
    <div
      style="height: 100%; width: 100%; cursor: pointer"
      title="无人机"
      @click="openList($event)"
    >
      <svg
        version="1.1"
        id="Layer_1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        x="0px"
        y="0px"
        width="40px"
        height="40px"
        viewBox="0 0 40 40"
        enable-background="new 0 0 40 40"
        xml:space="preserve"
      >
        <image
          id="image0"
          width="40"
          height="40"
          x="0"
          y="0"
          href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAoCAQAAAAm93DmAAAABGdBTUEAALGPC/xhBQAAACBjSFJN
AAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAAAAmJLR0QA/4ePzL8AAAAHdElN
RQflCh4QCgCW4lNmAAAEnklEQVRIx52Wf0zUdRjH33fgCQcCiqIIpM0zt9iaoYZRk2qluVqUjWlz
rVas6TTdarnoh4WZ5sx+zflPaMbagkpdZhijHxRZxjAQqM1+CIoL5GdKyK/jXv3x/dy3g/th43O7
7Z738zzv733ueZ73cw4kSYrWauUrWynqUr0Oq0QDutpxapGylKQu1ajRRhFiDrWMPWe4AUV8PUxz
QHw9KyzcomsH+thDLh5uZRs9QB9ZYcmieA+AK3xFGdUMAz6KLMJoaoFfmReQkEEN0II7DOE+wMt2
Eo09kwMAbEBiLfAPc8elpNIGPBOSLgcf8MQ4dBswwBxxHNgdIm0LcCok4cfA0SDUwc/ADvEXsMyA
+xniiLloJuDDFYLwMnAXQiRyhAH2GrwAqBNeYAFCxJiKVeJGJACQGkQ3HYBEhJsqAHxMQohFQL9T
f0tKkyQNqlqSdKcOabJG9JtQb1D3RUmSvHLrqHIlSVUasb0OUQHsMU9PtvuxkjhmUByyZbopYCrf
mciTTDOex4BG8QhwiWsMmMRJE1jDrDBNM58MmkxUNQk2fgJ4XUyiCWgi3cCJNuU5FockXEqrifiB
OBvdDAxxrVXPHqCXIhaTxlSm0WASBnmaqDFk0Wxh2Hgb7MaOZxc+oBAzy5n8Yk9lKx7SabftWlbi
QAgn91Nv4xdIR2zkXcq5BMBeHH5C4eJxKugHBjiIWMZIwOi3UcU3XAxAhrgFsd62m1ljMTkY2xSx
tmxtVVEE6SrUa5Lu0Y2KV7d+0gmNmr4hXMok1SnTfG7VF3JqpWYbu15L5A2TF0HxHjTXOYCLNGYR
S5lB8sJnRSKMohtowcUORvGxEzdtQDvOiRGKGqCYDHxmZj2UAN9HynFG3BouSVHy2XPqn+RIJ8LT
oukB2nCzGx+wjyl0Ah0TvXK+KcFnJJHGXBI5ZpD8iRC6OGO3bSelfEKPbTcaBfwfhHH2uL9JpLMV
IWazklXcTEwowtsppQuAFtLIM5X1j14lXwbMN3i5DSefGqufYr8AWmQxZg1azbEWD922XU2uEQex
wpY26MCDm2PUmq/Ry91+wijKAR9lrCCNZNI5a5KGKRxXUSebGDDe340EO7iDBmCQbIvwJaCfe23N
9qvhn9wU8odfaP8JCVTECuAsLpFAH7DeOKZzyl4BM8JUMoaUgEUx1aDJdAMPWd3WbC6WSqMJrCAe
8TxLCO6DRuYRR4WJrCPFeN4BSsUu4KCBfjRBh3EhXgXWBRFmAecQLsrtzWJ5VgOnnUqS1C5JitFS
SdLnWqNhSfMlJQbNaqx5D+sBVUiSshUtSeqTFOtUV8Cif0uX9IHyNSxJSpfUGUR4XtIMpUga0ip9
pF69YcT2ekmt4j6gI7DXzSuVEWBhiKL8AbwQhDqoA54VMbQDLwcFvA/Uh6zyZqAHzzh0EzBIhhDr
AK/dOFb77gR8LA9JOJkm4Dw5AULyHKPAi1ZjOygB4FseJYscNnIagO1hlchDC+Dja17hKd7mHADF
OP2z7GTbmD0MV3gyglKKmXzIaEB8Fxssz39r9DoVaLky5FWzjmu/LlxV7BcoT5maoouq0SFdtsB/
AT39FIa1PeSAAAAAJXRFWHRkYXRlOmNyZWF0ZQAyMDIxLTEwLTMwVDEzOjEwOjAwKzAzOjAw3ref
ZgAAACV0RVh0ZGF0ZTptb2RpZnkAMjAyMS0xMC0zMFQxMzoxMDowMCswMzowMK/qJ9oAAAAASUVO
RK5CYII="
        />
      </svg>
    </div>
    <div class="drone-list-wrap">
      <pop-up-layer
        :show="listShow"
        :setStyles="{ zIndex: 9999 }"
        @doClose="listClose"
        title="无人机列表"
        ref="myPopUpLayer"
      >
        <template slot="content">
          <div class="drone-pop-content">
            <div class="content-opation">
              <p class="form-p">
                <label for="">名称</label>
                <input type="text" v-model="sendForm.name" />
              </p>
              <p class="form-p">
                <label for="">状态</label>
                <select
                  type="text"
                  v-model="sendForm.state"
                  v-if="statusList.length"
                >
                  <option v-for="i in statusList" :key="i.id">
                    {{ i.name }}
                  </option>
                </select>
              </p>
              <p class="btn" @click="toSearch">查询</p>
              <p class="btn" @click="doClearn">清空</p>
              <p class="btn" @click="patchOpenVideo">查看视频</p>
            </div>
            <div class="content-table-list">
              <Clist class="table-list" :columns="columns" :listData="listData">
                <template slot="checked" slot-scope="{ record, text, index }">
                  <div class="index-key">
                    <p
                      @click="changeCheckType(record, index)"
                      class="check-box"
                      :class="[record.checked ? 'haed-check' : '']"
                    ></p>
                  </div>
                </template>
                <template slot="operation" slot-scope="{ record, text, index }">
                  <div class="operation-divs">
                    <!-- <p class="btn-p" @click="showDetail(record)">查看</p> -->
                    <p class="btn-p" @click="showVideo(record, text, index)">
                      视频
                    </p>
                    <p class="btn-p" @click="positionMap(record, text, index)">
                      {{ record.isPointMap ? "已定位" : "定位" }}
                    </p>
                  </div>
                </template>
                <template slot="state" slot-scope="{ record }">
                  <div>
                    <p
                      style="color: green"
                      v-show="
                        String(record.state) === '1' ||
                        String(record.state) === '0'
                      "
                    >
                      {{ showStatus[record.state] }}
                    </p>
                    <p
                      style="color: red"
                      v-show="
                        String(record.state) === '-1' ||
                        String(record.state) === '2'
                      "
                    >
                      {{ showStatus[record.state] }}
                    </p>
                  </div>
                </template>
              </Clist>
            </div>
            <div class="table-pages">
              <ChangePage
                :total="total"
                v-model="currentPage"
                @changePages="changePages"
                :pageSize="300"
              />
            </div>
          </div>
        </template>
      </pop-up-layer>
      <videoShow ref="videoShow" />
    </div>
  </div>
</template>

<script>
import Clist from "@/components/APicture/c-table.vue";
import ChangePage from "@/components/APicture/changePage/index.vue";
import { getIdsmApi } from "@/api/idsm/index";
import videoShow from "./videoShow.vue";
export default {
  components: { Clist, ChangePage, videoShow },
  computed: {
    pushData() {
      return this.$store.getters.responeData;
    },
  },
  watch: {
    pushData: {
      handler(newVal, oldVal) {
        /*  console.log("testssss", newVal); */
        let currentNewVal = JSON.parse(JSON.stringify(newVal));
        if (currentNewVal.cmd) {
          let cmdCode = currentNewVal.cmd;
          switch (cmdCode) {
            case "JgPyUnnK": // 轨迹
              /* this.getLeftEventList(); */
              if (
                currentNewVal.data &&
                currentNewVal.data.APP_AIRCRAFT_STREAM_DTO &&
                currentNewVal.data.APP_AIRCRAFT_STREAM_DTO.length
              ) {
                /* console.log("currentNewVal", currentNewVal); */
                // this.doChangeState(currentNewVal.data.APP_LIST_DTO);
                this.drawRoute(currentNewVal.data.APP_AIRCRAFT_STREAM_DTO);
              }
              break;
            case "r77FxBoG": // 状态
              if (
                currentNewVal.data &&
                currentNewVal.data.APP_LIST_DTO &&
                currentNewVal.data.APP_LIST_DTO.length &&
                this.listShow === true
              ) {
                /* console.log("currentNewVal", currentNewVal); */
                this.doChangeState(currentNewVal.data.APP_LIST_DTO);
              }
              break;
            default:
              break;
          }
        }
      },
      deep: true,
    },
  },
  data() {
    return {
      parentDatas: {},
      listShow: false,
      sendForm: {
        name: "",
        state: "",
      },
      statusList: [
        {
          id: -1,
          name: "离线",
        },
        {
          id: 0,
          name: "在线",
        },
        {
          id: 1,
          name: "在线",
        },
        {
          id: 2,
          name: "离线",
        },
      ],
      showStatus: {
        "-1": "离线",
        0: "在线",
        1: "在线",
        2: "离线",
      },
      columns: [
        { title: "", textIndex: "checked", width: "5%" },
        { title: "序号", textIndex: "indexKey", width: "10%" },
        { title: "名称", textIndex: "name", width: "23%" },
        { title: "状态", textIndex: "state", width: "15%" },
        { title: "所属单位", textIndex: "unitName", width: "22%" },
        // { title: "事发时间", textIndex: "sfsj", width: "20%" },
        // { title: "预案等级", textIndex: "eventLevel", width: "15%" },
        { title: "操作", textIndex: "operation", width: "25%" },
      ],
      listData: [],
      total: 0,
      currentPage: 1,
      checkedList: [],
      routerGeometry: {},
    };
  },
  methods: {
    openList(e) {
      /*  console.log(e); */
      this.listShow = !this.listShow;
      if (this.listShow) {
        /*  console.log("window", window); */
        this.doClearn();
        // this.getList();
      } else {
        /*  console.log(this.listShow); */
      }
      this.clearRoute();
    },
    initData() {
      this.doClearn();
    },
    listClose() {
      this.listShow = false;
    },
    /* 查询 */
    toSearch() {
      this.total = 0;
      this.currentPage = 1;
      this.getList();
    },
    /* 清空 */
    doClearn() {
      this.total = 0;
      this.currentPage = 1;
      this.checkedList = [];
      for (let key in this.sendForm) {
        this.sendForm[key] = "";
        if (key === "state") {
          this.getList();
        }
      }
    },
    /* 查看 */
    showDetail(item) {},
    /* 获取分页 */
    changePages(pages) {},
    /* 获取列表 */
    getList() {
      let code = "jkx92oLu";
      let sendObj = {
        body: this.$filterParams({ ...this.sendForm }),
        page: this.currentPage,
        pageSize: 300,
      };
      getIdsmApi(code, sendObj)
        .then((res) => {
          console.log(res);
          if (res.success) {
            if (res.body && res.body.data && res.body.data.length) {
              this.routerGeometry = [];
              this.listData = res.body.data;
              res.body.data.map((i, k) => {
                i.indexKey =
                  this.currentPage === 1
                    ? k + 1
                    : (this.currentPage - 1) * 10 + (k + 1);
                i.isPointMap = false;
                i.isDisabled = true;
                if (i.deviceId) {
                  this.routerGeometry[i.deviceId] = [];
                }
                if (i.latitude && i.longitude) {
                  this.routerGeometry[i.deviceId].push(i.longitude, i.latitude);
                }
                if (this.checkedList.length) {
                  // 检查是否已经又选中，如果有，并符合条件的更改未选中状态
                  let saveFindItem = null;
                  saveFindItem = this.checkedList.find((fi, fk) => {
                    if (fi.deviceId === i.deviceId) {
                      return fi;
                    }
                  });
                  if (saveFindItem) {
                    i.checked = true;
                  } else {
                    i.checked = false;
                  }
                } else {
                  // 选中状态为false
                  i.checked = false;
                }
              });
            } else {
              this.listData = [];
            }
          } else {
            this.listData = [];
          }
        })
        .catch((error) => {
          if (error) {
            this.listData = [];
          }
        });
    },
    /* 根据推送消息处理无人机状态 */
    doChangeState(list) {
      if (list.length) {
        list.map((i, k) => {
          this.listData.find((item, keys) => {
            if (String(item.deviceId) === String(i.deviceId)) {
              this.listData[keys]["state"] = i.state;
              i.isDisabled =
                String(i.state) === "-1" || String(i.state) === "2"
                  ? true
                  : false;
              // this.listData[keys]["state"] = 0;
              // this.listData = JSON.parse(JSON.stringify(this.listData));
              /* console.log("changes", this.listData); */
            }
          });
        });
      }
    },
    /* 打开无人机视频 */
    showVideo(item) {
      let childrenList = [
        {
          ...item,
          toLink: "loadingEndSuccess",
        },
      ];
      this.openVideoModel(childrenList);
    },
    /* 批量打开视频 */
    async patchOpenVideo() {
      if (this.checkedList.length) {
        let saveList = [];
        await this.checkedList.map((i, k) => {
          saveList.push({
            ...i,
            toLink: "loadingEndSuccess",
          });
        });
        this.openVideoModel(saveList);
      } else {
        this.$MyMessage.warning("请选中视频！");
      }
    },
    /* 打开视频组件 */
    openVideoModel(list) {
      this.$refs.videoShow.$emit("show", { listDatas: list });
    },
    /* 选中 */
    async changeCheckType(i, k) {
      /*  console.log(k); */
      if (!i.checked && this.checkedList.length === 4) {
        // 如果选中等于4 直接退出
        this.$MyMessage.warning("最多播放4路视频！");
        return false;
      }
      this.listData[k]["checked"] = !i.checked;
      if (this.listData[k]["checked"]) {
        // 选中时-checkedList
        this.checkedList.push(i);
      } else {
        // 取消选中时-checkedList
        let currentKeys = null;
        let obj = await this.checkedList.find((item, keys) => {
          if (item.deviceId === i.deviceId) {
            currentKeys = keys;
            return item;
          }
        });
        this.checkedList.splice(currentKeys, 1);
        /*  console.log(this.checkedList); */
      }
      this.listData = JSON.parse(JSON.stringify(this.listData));
    },
    /*定位 */
    positionMap(item, text, index) {
      /* console.log(item, text, index); */
      if (item.isPointMap) {
        this.listData[index]["isPointMap"] = false;
        window.pGzznCore.pointLayerRemove({ type: "defaultType" + item.sid });
        this.listData = JSON.parse(JSON.stringify(this.listData));
      } else {
        this.listData[index]["isPointMap"] = true;
        window.pGzznCore.pointLayerRemove({ type: "defaultType" + item.sid });
        let lists = [
          {
            sid: item.sid,
            teamId: item.deviceId, // 设备ID
            name: item.name, // 无人机名称
            teamName: item.unitName, // 所属单位
            lon: String(item.longitude),
            lat: String(item.latitude),
            ...item,
          },
        ];
        let showInfo = [
          { title: "名称", textIndex: "name" },
          { title: "播放地址", textIndex: "pullHttp" },
          { title: "所属单位", textIndex: "unitName" },
        ];
        let objs = {
          imgUrl: `./big-screen/gzznGIS/Image/icon_UAV.png`,
          /* imgUrlObj: { keys: "level", start: `gzznGIS/Image/icon_UAV.png` }, */
          imgSize: { width: 32, height: 32 },
          type: "defaultType" + item.sid,
          info: showInfo,
          layerName: "无人机",
        };
        window.pGzznCore.setPointLayerToMap(lists, objs);
        this.listData = JSON.parse(JSON.stringify(this.listData));
      }
    },
    ceatePoint(item, type, isFlagFlyTo = false) {
      pGzznCore.pointLayerRemove({ type: type });
      let showInfo = [
        { title: "名称", textIndex: "name" },
        { title: "播放地址", textIndex: "pullHttp" },
        { title: "所属单位", textIndex: "unitName" },
      ];
      let objs = {
        imgUrl: `./big-screen/gzznGIS/Image/icon_UAV.png`,
        /* imgUrlObj: { keys: "level", start: `gzznGIS/Image/icon_UAV.png` }, */
        imgSize: { width: 32, height: 32 },
        type: type,
        info: showInfo,
        lonLat: { lon: "lng", lat: "lat" },
        layerName: "无人机",
        isFlagFlyTo: isFlagFlyTo,
        rotation: { keys: "aircraftYaw" }, //
      };
      pGzznCore.setPointLayerToMap([item], objs);
    },
    /* 绘制轨迹 */
    drawRoute(data) {
      /* console.log(data, "data"); */
      if (
        data &&
        data.length &&
        this.listData.length &&
        this.checkedList.length
      ) {
        data.map((item, k) => {
          let items = this.routerGeometry[item.deviceId];
          // if (k == 1) {
          //   item.lng = parseFloat(items[items.length - 2]) + 0.005;
          //   item.lat = parseFloat(items[items.length - 1]) + 0.002;
          // } else {
          //   item.lng = parseFloat(items[items.length - 2]) + 0.002;
          //   item.lat = parseFloat(items[items.length - 1]);
          // }
          let isChecked = pGzznCore.findArray(
            this.checkedList,
            "deviceId",
            item.deviceId
          );
          if (
            item.lng &&
            item.lat &&
            item.deviceId &&
            items &&
            (item.lng != items[items.length - 2] ||
              item.lat != items[items.length - 1]) &&
            isChecked
          ) {
            this.routerGeometry[item.deviceId].push(item.lng, item.lat);
            var lists = this.routerGeometry[item.deviceId];
            let rescord = pGzznCore.deepClone(item);
            if (lists.length == 4) {
              rescord.lng = lists[lists.length - 4];
              rescord.lat = lists[lists.length - 3];
              this.ceatePoint(
                rescord,
                "defaultTypeUAVStart" + rescord.deviceId
              );
            }

            this.ceatePoint(
              rescord,
              "defaultTypeUAVEnd" + rescord.deviceId,
              true
            );
            pGzznCore.drawLineToMap(
              [
                lists[lists.length - 4],
                lists[lists.length - 3],
                lists[lists.length - 2],
                lists[lists.length - 1],
              ],
              [0, 255, 255, 1],
              true,
              { type: "drawUAVRoute" }
            );
          }
        });
      }
    },
    clearRoute() {
      for (let keys in this.routerGeometry) {
        pGzznCore.pointLayerRemove({ type: "defaultTypeUAVStart" + keys });
        pGzznCore.pointLayerRemove({ type: "defaultTypeUAVEnd" + keys });
      }

      pGzznCore.drawLineRemove({ type: "drawUAVRoute" });
    },
  },
};
</script>


<style lang="less" scoped>
@import './index.less';
.drone-icon {
  /* top: 382vh * @h;
  right: 1029vw * @w; */
  /* top:0px;
  left:1100px; */
  svg {
    width: 100%;
    height: 100%;
  }
}
</style>
