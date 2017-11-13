<template>
  <div id="app">
    <header>
      <div class="setting">
        <a href="#/setting">
          <img src="./img/setting.png" alt="setting-btn">
        </a>
      </div>
      <div class="location">
        <a href="#/detail">
          <img src="./img/location-icon.png" alt="location-btn">
        </a>
      </div>
      <h1><a href="#/home">{{title}}</a></h1>
    </header>
    <div class="content-wrap">
      <router-view/>
    </div>
  </div>

</template>

<script>
  export default {
    name: 'app',
    data: function () {
      return {
        title: 'Weather'
      }
    },

  }

</script>

<style scoped lang="less">
  @import "less/common.css";

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    header {
      background-color: #36235f;
      height: 44px;
      position: fixed;
      left: 0;
      right: 0;
      z-index: 100;
      .setting {
        float: left;
      }
      .location {
        float: right;
      }
      img {
        display: inline-block;
        height: 28px;
        width: 28px;
        padding: 8px ;
      }
      h1 {
        font-weight: 500;
        text-align: center;
        line-height: 44px;
        font-size: 18px;
        a {
          color: #fff;
        }
      }
    }
    .content-wrap {
      padding-top: 44px;
    }
  }
</style>
