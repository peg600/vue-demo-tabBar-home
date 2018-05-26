<template>
    <div class="wrapper">
      <div class="content">
        <div class="classify">
          <img src="./分类@2x.png" class="up">
          <img src="./分类-字@2x.png" class="dowm">
        </div>
        <div class="camera">
          <img src="./椭圆1拷贝@2x.png" >
        </div>
        <div class="shopcart">
          <img src="./购物车@2x.png" class="up">
          <img src="./购物车-字@2x.png" class="down">
        </div>
      </div>
    </div>
</template>

<script>
    export default {
      name: "buttons",
      props: {

      },
      data() {
        return {
          picClassify: {
            icon:"./分类@2x.png",
            word:"./分类-字@2x.png"
          },
          picCamera: {
            icon:"./椭圆1拷贝@2x.png",
          },
          picShopcart: {
            icon:"./购物车@2x.png",
            word:"./购物车-字.@2x.png"
          }
        }
      }
    }
</script>

<style scoped>
  .wrapper {
    position: fixed;
    bottom: 0;
    width: 100%;
    height: 110px;
    box-sizing: border-box;
    z-index: 30;
    background-color: rgba(12,76,212,.2);
  }

  .content {
    display: flex;
    position: absolute;
    flex-direction: row;
    width: 100%;
    top: 0;
    bottom: 50px;
    background-color: aqua;
  }

  .classify {
    height: 41px;
    margin-top: 18px;
    margin-bottom: 20px;
    background-color: crimson;
  }

  .camera {
    width: 60px;
    height: 60px;
    background-color: darkblue;
  }

  .shopcart {
    height: 41px;
    margin-bottom: 20px;
    background-color: darkseagreen;
  }


</style>
