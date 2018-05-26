<template>
    <div class="wrapper">
      <div class="content">
        <div class="classify">
          <img src="./分类@2x.png" height="23" class="pic-up">
          <img src="./分类-字@2x.png" height="13">
        </div>
        <div class="camera">
          <img src="./椭圆1拷贝@2x.png" height="60">
        </div>
        <div class="shopcart">
          <img src="./购物车@2x.png" height="23" class="pic-up">
          <img src="./购物车-字@2x.png" height="13">
        </div>
      </div>
    </div>
</template>

<script>
    export default {
      name: "buttons",
      props: {
        dpr:{
          type:Number
        }
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

  img {
    display: block;
    margin: auto;
  }

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
    position: absolute;
    flex-direction: row;
    justify-content: center;
    width: 100%;
    top: 0;
    bottom: 50px;
    text-align: center;
    background-color: aqua;
  }

  .classify {
    display: inline-block;
    vertical-align: bottom;
    height: 41px;
    margin-top: 9px;
    margin-bottom: 10px;
    margin-right: 60px;
    background-color: crimson;
  }

  .camera {
    display: inline-block;
    vertical-align: bottom;
    width: 60px;
    height: 60px;
    background-color: darkblue;
  }

  .shopcart {
    display: inline-block;
    vertical-align: bottom;
    height: 41px;
    margin-top: 9px;
    margin-bottom: 10px;
    margin-left: 60px;
    background-color: darkseagreen;
  }

  .pic-up {
    margin-bottom: 5px;
  }



</style>
