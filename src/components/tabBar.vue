<template>
  <div class="tab-wrapper" ref="tabWrapper" v-show="show">
    <div class="tab-content" ref="itemWrapper">
      <ul class="item-list" v-if="items" ref="itemList">
        <li class="clear">
          <img  class="img-clear" :src="dsr>2 ? require('./关闭(1)@2x.png') : require('./关闭(1)@3x.png')">
        </li>
        <li class="item" @click="showItemList($event,item_message)">
          热销
        </li>
        <li class="item" :class="{'active-item': activeType === item_message.message.type}" v-for="(item_message,item,index) in items"
            @click="showItemList($event,item_message)">
          <div class="item-content">
            <span class="item-name" >{{item_message.message.name}}</span>
              <!--<img class="item-avatar" v-if="item_message.message.avatar"
                   :src="item_message.message.avatar" height="20px" width="20px"> -->
          </div>
        </li>
      </ul>
    </div>
    <list :itemMessage="itemMessage" @touchmove.prevent></list>
  </div>
</template>
<script>
  import BScroll from "better-scroll"
  import list from "./list.vue"

  export default {
    name: "tabBar",
    props:{
      show:{
        type:Boolean
      },
      items:{
        type:Object
      },
      dsr:{
        type:Number
      }
    },
    data() {
      return {
        activeType:0,
        itemMessage:{}
      }
    },
    watch: {
      "items"() {
        this.$nextTick(() => {
          this._initScroll();
        });
      }
    },
    mounted() {
      this.$nextTick(() => {
        this._initScroll();
      });
    },
    methods:{
      _initScroll() {
        if (this.items) {
          let itemsArray = Object.keys(this.items);
          /*let screenWidth = document.body.scrollWidth;
          let margin = 6;
          let itemWidth = (screenWidth-2*margin)/4;*/
          let width = 67 * (itemsArray.length+1) + 40;    // 计算所有图片总宽度，即ul宽度
          this.$refs.itemList.style.width = width + "px";    // 为图片列表设置宽度，只有宽度大于容器才能滚动
          this.$nextTick(() => {
            if (!this.itemScroll) {
              this.itemScroll = new BScroll(this.$refs.itemWrapper, {
                bounceTime: 300,
                scrollX: true,                        // 横向滚动
                eventPassthrough: "vertical"        // 在横向滚动时忽略纵向滚动
              });
            } else {
              this.itemScroll.refresh();
            }
          });
        }
      },

      showItemList(e,item_message) {
        this.itemMessage = item_message;
        this.activeType = item_message.message.type;
      }



      /*
      showItemList(e,item_message) {
        //if(this.activeType && this.activeType === item_message.message.type) {
          //this.showList = false;           // 若点击的是展示状态的tab，则取消展示状态并收起列表
          //this.activeType = 0;
          //this.itemMessage = {};
          //this.$emit("hide-list");
          //this.$refs.tabWrapper.style.height = 50+"px";
          //console.log(this.itemMessage,this.showList,this.activeType);
        //}else{                              // 若点击非展示状态的tab，将其标记为展示中并弹出列表
          this.activeType = item_message.message.type;
          //this.showList = true;
          this.itemMessage = item_message;// 准备将itemMessage传给list组件
          this.$emit("show-list");
          //this.$refs.tabWrapper.style.height = 220+"px";
          console.log(this.itemMessage,this.show,this.activeType);
        //}
      }*/
    },
    components:{
      list
    }
  }
</script>

<style scoped>

  .tab-wrapper {
    position: fixed;
    bottom: 0;
    width: 100%;
    height: 230px;
    box-sizing: border-box;
    transform: translate(0,0%);
    overflow: hidden;
    white-space: nowrap;
    z-index: 30;
    background-color: rgba(0,0,0,.3);
  }

  .tab-content {
    height: 40px;
    width: 100%;
  }

  .item-list {
    font-size: 0;
    padding-left: 0;
    color: rgb(255,255,255);
    box-sizing: border-box;
  }

  .clear {
    display: inline-block;
    height: 40px;
    line-height: 40px;
    width: 40px;
    text-align: center;
    font-size: 15px;
    list-style-type: none;
    vertical-align: middle;
  }

  .img-clear {
    height: 20px;
    width: 20px;
    margin: 0 auto;
  }

  .item {
    display: inline-block;
    height: 40px;
    line-height: 40px;
    width: 67px;
    text-align: center;
    font-size: 15px;
    list-style-type: none;
  }



  .item:last-child {
    margin-right: 0;
    border-right: none;
  }

  .item-name,.item-avatar {

  }

  .active-item{
    color: rgb(255,189,69);
  }
</style>
