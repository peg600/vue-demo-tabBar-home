<template>
  <div class="tab-wrapper" ref="tabWrapper" v-show="show">
    <div class="tab-content" ref="itemWrapper">
      <ul class="item-list" v-if="items" ref="itemList">
        <li class="clear">
          <img  class="img-clear" :src="dsr>2 ? require('./关闭(1)@2x.png') : require('./关闭(1)@3x.png')">
        </li>
        <li class="item" :class="{'active-item': activeType === item_message.id}" v-for="(item_message,item,index) in items"
            @click="showItemList($event,item_message,index)">
          <div class="item-content">
            <span class="item-name" >{{item_message.name}}</span>
          </div>
        </li>
      </ul>
    </div>
    <div class="goods-content">
      <div class="goods-wrapper" ref="outWrapper">
        <div class="goods-type-wrapper" ref="innerWrapper" :style="this.listWidth">
          <div class="goods-type" v-for="(item_message,item_id,index) in items" ref="goodsType" :style="screenWidth" >
            <ul class="goods-list" :class="item_id">
              <li class="goods-item" v-for="goods in listArray[index+1]" @click="selectitem($event,goods,index)">
                <a class="goods-link">
                  <!--<span class="item-name">{{item.name}}</span>-->
                  <img :src="goods.goods_thumb" alt="item.name" class="item-img"
                       height="75px" width="75px" >
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  import BScroll from "better-scroll"

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
      },
      listArray:{
        type:Array
      }
    },
    data() {
      return {
        activeType:1,
        itemMessage:{},
        listWidth:"",
        screenWidth:"",
        fullWidth:0,
        selected:[]
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
          this.fullWidth = document.body.scrollWidth;
          this.screenWidth = `width: ${document.body.scrollWidth}px;`;
          let width = 67 * (itemsArray.length+1) + 40;    // 计算所有图片总宽度，即ul宽度
          this.$refs.itemList.style.width = width + "px";    // 为图片列表设置宽度，只有宽度大于容器才能滚动
          this.listWidth = `width: ${this.fullWidth * (itemsArray.length+1)}px`;
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
            if (!this.goodsScroll) {
              this.goodsScroll = new BScroll(this.$refs.outWrapper, {
                preventDefault: true,
                scrollX: true,
                scrollY:true
              });
            } else {
              this.goodsScroll.refresh();
            }
          });
        }
      },

      showItemList(e,item_message,index) {
        this.activeType = item_message.id;
        let goodsList = this.$refs.goodsType;
        let el = goodsList[index];
        this.goodsScroll.scrollToElement(el,300);
      },

      selectitem(e) {
        console.log(123);
        if(this.select[index+1]===goods.id) {
          this.select[index+1] = null;
          e.target.setAttribute("class","goods-item");

        }else{
          this.selected[index+1] = goods.id;
          e.target.setAttribute("class","goods-item selected-item");
          console.log(this.selected)
        }
      }

      /*
      showItemList(e,item_message) {
        //if(this.activeType && this.activeType === item_message.id) {
          //this.showList = false;           // 若点击的是展示状态的tab，则取消展示状态并收起列表
          //this.activeType = 0;
          //this.itemMessage = {};
          //this.$emit("hide-list");
          //this.$refs.tabWrapper.style.height = 50+"px";
          //console.log(this.itemMessage,this.showList,this.activeType);
        //}else{                              // 若点击非展示状态的tab，将其标记为展示中并弹出列表
          this.activeType = item_message.id;
          //this.showList = true;
          this.itemMessage = item_message;// 准备将itemMessage传给list组件
          this.$emit("show-list");
          //this.$refs.tabWrapper.style.height = 220+"px";
          console.log(this.itemMessage,this.show,this.activeType);
        //}
      }*/
    },
    components:{

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


  .goods-content {
    overflow: hidden;
  }

  .goods-wrapper {
    position: absolute;
    width: 100%;
    top: 40px;
    bottom: 0;
    overflow: hidden;
    font-size: 0;
    border-top: 2px solid rgba(242,242,242,.15);
    box-sizing: border-box;
    background-color: rgba(0,0,0,.3);
  }

  .goods-type-wrapper {

  }

  .goods-type {
    display: inline-block;
    width: 375px;
    min-height: 188px;
    margin: 0;
    padding: 0;
  }

  .goods-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0;
    padding: 0;
  }

  .goods-item {
    text-align: center;
    list-style-type: none;
    flex: 0 75px;
  }

  .selected-item {
    border-radius: 10px;
    border: 2px solid rgb(255,189,69);
  }

</style>
