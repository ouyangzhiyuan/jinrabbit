<template>
  <!--在视频外面加一个容器-->
  <div class="input_video">
    <video-player
      class="video-player vjs-custom-skin"
      ref="videoPlayer"
      :playsinline="true"
      :options="playerOptions"
    ></video-player>
      <vue-baberrage
        :isShow="barrageIsShow"
        :barrageList="barrageList"
        :maxWordCount="maxWordCount"
        :throttleGap="throttleGap"
        :loop="barrageLoop"
        :boxHeight="boxHeight"
        :messageHeight="messageHeight"
      ></vue-baberrage>
    </div>
</template>
<script>
import Vue from "vue";
import { vueBaberrage, MESSAGE_TYPE } from "vue-baberrage";
Vue.use(vueBaberrage);
export default {
  name: "BusImg",
  data() {
    return {
      // 视频播放
      playerOptions: {
        playbackRates: [0.5, 1.0, 1.5, 2.0], //可选择的播放速度
        autoplay: false, //如果true,浏览器准备好时开始回放。
        muted: false, // 默认情况下将会消除任何音频。
        loop: false, // 视频一结束就重新开始。
        preload: "auto", // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
        language: "zh-CN",
        aspectRatio: "16:10", // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
        fluid: true, // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
        sources: [
          {
            type: "",
            src:
              "" //url地址
          }
        ],
        poster:
          "http://www.cgdream.com.cn/data/attachment/forum/201811/06/163249ent52ff4bng2gk2b.jpg", //你的封面地址
        notSupportedMessage: "此视频暂无法播放，请稍后再试", //允许覆盖Video.js无法播放媒体源时显示的默认信息。
        controlBar: {
          timeDivider: true, //当前时间和持续时间的分隔符
          durationDisplay: true, //显示持续时间
          remainingTimeDisplay: false, //是否显示剩余时间功能
          fullscreenToggle: true //全屏按钮
        }
      },
      msg: "",
      barrageIsShow: true,
      messageHeight: 3,
      boxHeight: 50,
      barrageLoop: true,
      maxWordCount: 3,
      throttleGap: 5000,
      barrageList: []
    };
  },
  mounted() {
    this.addToList();
  },
  methods: {
    addToList() {
      let list = [
        {
          msg: "你说啥",
          id: 1,
          avatar:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3064584167,3502823640&fm=26&gp=0.jpg",

          time: 3
          ,barrageStyle: "red"
        },
        {
          msg: "你说啥",

          id: 2,
          avatar:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3064584167,3502823640&fm=26&gp=0.jpg",

          time: 8
          ,barrageStyle: "green"
        },
        {
          id: 3,
          msg: "你说啥",

          avatar:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3064584167,3502823640&fm=26&gp=0.jpg",

          time: 10
          ,barrageStyle: "normal"
        },
        {
          id: 4,
          msg: "你说啥",

          avatar:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3064584167,3502823640&fm=26&gp=0.jpg",

          time: 5
          ,barrageStyle: "blue"
        },
        {
          id: 5,

          msg: "wobuxi",

          avatar:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3064584167,3502823640&fm=26&gp=0.jpg",

          time: 6
          ,barrageStyle: "red"
        },
        {
          id: 6,
          msg: "gun",

          avatar:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3064584167,3502823640&fm=26&gp=0.jpg",

          time: 12
          ,barrageStyle: "normal"
        },
        {
          msg: "pihua",
          id: 7,
          avatar:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3064584167,3502823640&fm=26&gp=0.jpg",

          time: 5
          ,barrageStyle: "red"
        },
        {
          msg: "你说啥",
          id: 8,
          avatar:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3064584167,3502823640&fm=26&gp=0.jpg",
          time: 5
          ,barrageStyle: "normal"
        },
        {
          msg: "你说啥",
          id: 9,
          avatar:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3064584167,3502823640&fm=26&gp=0.jpg",
          time: 8
          ,barrageStyle: "red"
        },
        {
          msg: "你说啥",
          id: 10,
          avatar:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3064584167,3502823640&fm=26&gp=0.jpg",
          time: 10
          ,barrageStyle: "yellow"
        }
      ];
      list.forEach(v => {
        this.barrageList.push({
          id: v.id,
          avatar: v.avatar,
          msg: v.msg,
          time: v.time,
          type: MESSAGE_TYPE.NORMAL,
        //   barrageStyle: v.barrageStyle
        });
      });
    }
  }
};
</script>
<style>
.input_video {
  width: 100%;
  margin: 0 auto;
  position: relative;
  z-index: 2;
}
.video-player{
    border: 1px solid red;
    position: relative;
    z-index: 2;
}
.danmu {
  border: 1px solid red;
  background: red;
}
.blue {
  border-radius: 100px;
  background: #e6ff75;
  color: red;
}
.green {
  border-radius: 100px;
  background: #75ffcd;
  color: red;
}
.red {
  border-radius: 100px;
  background: #e68fba;
  color: red;
}
.yellow {
  border-radius: 100px;
  background: #dfc795;
  color: red;
}
.baberrage-stage {
  position: absolute;
  width: 100%;
  height: 100px;
  border: 1px solid red;
  overflow: hidden;
  top: 0;
  z-index: 3;
}
</style>