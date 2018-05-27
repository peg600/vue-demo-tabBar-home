<template>
  <div class="goods-content">
    <div class="goods-wrapper" ref="outWrapper">
      <ul class="goods-list">
        <li class="goods-item" v-for="(item,index) in itemMessage.goods" ref="listItem">
          <a class="goods-link">
            <!--<span class="item-name">{{item.name}}</span>-->
            <img :src="item.avatar" alt="item.name" class="item-img"
            height="75px" width="75px" >
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

    import BScroll from "better-scroll"

    export default {
      name: "list",
      props:{
        itemMessage:{
          type:Object
        },
        show:{
          type:Boolean
        }
      },
      data() {
        return {
          selected:{}
        }
      },

      watch: {
        "itemMessage"() {
          this.$nextTick(() => {
            this._initScroll();
          });
        }
      },
      mounted() {
        this.$nextTick(() => {
          this._initScroll();
        })
      },

      methods:{
        _initScroll() {
          this.$nextTick(() => {
            if (!this.scroll) {
              this.scroll = new BScroll(this.$refs.outWrapper, {
                preventDefault: true,
                scrollX:true,
                scrollY:true,
              });
            } else {
              this.scroll.refresh();
            }
          })
        },

        initSelected() {

        }
      }
    }
</script>

<style scoped>

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


</style>
