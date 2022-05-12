<template>
  <div class="gifComponents">
    <div class="imgbox">
      <img
        id="example1"
        :src="imgUrl"
        :rel:animated_src="imgUrlGIF"
        rel:auto_play="0"
        width="375"
        @load="InitSuperGif"
      />
    </div>

    <div class="Buttonbox">
      <div
        v-for="(item, index) in tabrooms"
        :key="index"
        class="itembox"
        @click="tabClickfun(item, index)"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>
<script>
import SuperGif from "libgif";
export default {
  name: "gifComponents",
  data() {
    return {
      tabrooms: ["Pause", "Play", "Restart", "Step forward", "Step back"],
      imgUrl: require("@/assets/img/index1.jpg"),
      imgUrlGIF: require("@/assets/img/index.gif"),
      sup1: null,
    };
  },
  mounted() {
    // this.InitSuperGif();
  },
  methods: {
    InitSuperGif() {
      var that = this;
      console.log("SuperGif", SuperGif);
      // 通过异步函数，获取gif文件
      var sup1 = new SuperGif({
        gif: document.getElementById("example1"),
        on_end(res){
          console.log(res);
          that.sup1.pause();
        }
      });
      sup1.load();
      that.sup1 = sup1;
    },
    tabClickfun(item, index) {
      switch (item) {
        case "Pause":
          this.sup1.pause();
          break;
        case "Play":
          this.sup1.play();
          console.log(this.sup1.get_length());
          break;
      }
      // if (item === "Pause") {
      //   this.sup1.pause();
      // } else if (item === "Play") {
      //   this.sup1.play();
      // } else if (item === "Restart") {
      //   this.sup1.move_to(0);
      // } else if (item === "Step forward") {
      //   this.sup1.move_relative(1);
      // } else if (item === "Step back") {
      //   this.sup1.move_relative(-1);
      // }
    },
  },
};
</script>

<style lang="scss">
.gifComponents {
  box-sizing: border-box;
  width: 100%;
  margin-top: 30px;
  canvas{
    width: 100% !important;
    height: 100%;
  }
  .imgbox {
    width: 100%;
  }
  .Buttonbox {
    display: flex;
    margin-top: 30px;
    flex-wrap: wrap ;
    width: 100%;
    .itembox {
      box-sizing: border-box;
      width: 33.3333%;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      background: coral;
      color: #fff;
      padding: 10px;
      &:hover {
        background: rgb(219, 148, 122);
      }
    }
  }
}
</style>