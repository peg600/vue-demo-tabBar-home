<template>
  <div class="wrapper">
    <div class="content">
      <navBar :dpr="dpr" @show-list="showList" :show="show"></navBar>
      <div class="main">
      </div>
    </div>
    <buttons :dpr="dpr" @show-list="showList" :show="show"></buttons>
    <tabBar :items="items" :show="show" ></tabBar>
  </div>

</template>

<script>
import axios from "axios"
import navBar from "./components/navBar.vue"
import buttons from "./components/buttons.vue"
import tabBar from "./components/tabBar.vue"

export default {
  name: 'App',
  data() {
    return {
      dpr:1,
      items:{},
      response:{},
      show:false
    }
  },
  created() {
    axios.get("../static/standard1.json").then((response) => {      //@touchmove.prevent
      response = response.data;
      this.items = response.list;
      console.log(this.items)
    });
    this.dpr=window.devicePixelRatio;
  },
  methods:{
    showList() {
      this.show = true;
      axios.get("../static/standard1.json").then((response) => {      //@touchmove.prevent
        response = response.data;
        this.items = response.list;
        console.log(this.items)
      });
    },
    hideList() {
      this.show = false;
    }
  },
  components:{
    navBar,
    buttons,
    tabBar
  }
}
</script>

<style>

html,body {
  height: 100%;
  margin: 0;
  padding: 0;
  overflow: hidden;
  box-sizing: border-box;
  background-image: url("./background.jpg");
}

.wrapper {
  height: 100%;
  width: 100%;
}

.content {
  position: absolute;
  display: flex;
  top: 0;
  bottom: 0;
  max-height: 100%;
  width: 100%;
  flex-direction: column;
}

.main {
  flex: 1;
  box-sizing: border-box;
  width: 100%;
  overflow: auto;
  z-index: 5;
}



</style>
