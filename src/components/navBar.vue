<template>
    <div class="wrapper">
      <div class="content">
        <ul class="nav-wrapper" @click="showList($event)">
          <li class="nav-item">
            <img class="pic" :src="all">
            <img v-show="showList" :src="current_dot" alt="" class="dot">
          </li>
          <li class="nav-item">
            <img class="pic" :src="recommend">
          </li>
          <li class="nav-item">
            <img class="pic" :src="change">
          </li>
          <li class="nav-item">
            <img class="pic" :src="share">
          </li>
        </ul>
      </div>
    </div>
</template>

<script>
    export default {
      name: "navBar",
      props:{

        showList: {
          type: Boolean
        }
      },
      data() {
        return {
          dpr:1,
          all: require("./全部@2x.png"),
          recommend:require("./推荐@2x.png"),
          change:require("./换一批@2x.png"),
          share:require("./分享@2x.png"),
          current_dot:require("./椭圆1@2x.png"),
        }
      },
      created() {
        if(dpr>2) {
          this.all = require("./全部@3x.png");
          this.recommend = require("./推荐@3x.png");
          this.change = require("./换一批@3x.png");
          this.share = require("./分享@3x.png");
          this.current_dot = require("./椭圆1@3x.png");
        }
      }
    }
</script>

<style scoped>
  .wrapper {
    flex: 0 42px;
    width: 100%;
    margin: 0;
    padding: 0;
    z-index: 10;
    background-color: darkmagenta;
  }

  .content {

    height: 42px;
    width: 100%;
  }

  .nav-wrapper {
    padding: 0;
    margin: 0;
    height: 42px;
    line-height: 42px;
    text-align: center;
    font-size: 0;
    vertical-align: middle;
  }

  .nav-item {
    display: inline-block;
    box-sizing: border-box;
    height: 42px;
    width: 25%;
    padding: 12px 0;
    line-height: 18px;
    text-align: center;
    vertical-align: middle;
    list-style-type: none;
    color: rgb(255,255,255);
  }

  .pic {
    height: 18px;
  }


</style>
