<template>
  <div class="wrapper">
    <div class="content">
      <navBar :dpr="dpr"></navBar>
      <div class="main">
      </div>
    </div>
    <buttons :dpr="dpr"></buttons>
    <tabBar :items="items" :showList="showList" ></tabBar>
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
      showList:false
    }
  },
  created() {
    axios.get("../static/test.json").then((response) => {      //@touchmove.prevent
      response = response.data;
      this.items = response.items;
    });
    this.dpr=window.devicePixelRatio;
  },
  methods:{

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
  background-color: rgba(123,255,255,.2);
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
  background-color: rgba(184,165,212,.2);
}



</style>
