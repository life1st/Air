<template>
  <div id="app">
    <header>
      <div class="setting">
        <router-link to="/setting">
          <img src="./img/setting.png" alt="setting-btn">
        </router-link>
      </div>
      <div class="location">
        <a @click="clearData()">
          <img src="./img/location-icon.png" alt="location-btn">
        </a>
      </div>
      <h1><a href="#/">{{main.title}}</a></h1>
    </header>
    <div class="content-wrap">
      <router-view/>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'app',
    data: function () {
      return {
        main: {
          title: 'Weather',
          date: ''
        }
      }
    },
    mounted() {
      var _this = this
      this.clearData = function () {
        if (confirm('是否重新获取数据？')){
          localStorage.clear();
          window.location.reload();
        }
      }
/*      this.toData()
        .then(function (res) {
          var main = _this.main;
          console.log(res)
          main.title = res.data.city
          console.log(main.date)
        })
        .catch(function (err) {
          console.log(err)
        })*/
    },
    methods: {
/*      toData: function() {
        var amapKey = 'a75aef737f1db811578d960310aba54e';//高德API key
        var res = new Promise(function (resolve,reject){
          if (localStorage.getItem('city') &&
            new Date().getTime() - localStorage.getItem('time') < 36000000){
            console.log('old city data')
            var res = JSON.parse(localStorage.getItem('city'))
            resolve(res)
          }else {
            axios.get('http://restapi.amap.com/v3/ip?key=' + amapKey)
              .then(function (res) {
                console.log('new city data')
                localStorage.setItem('city',JSON.stringify(res))
                resolve(res)
              })
              .catch(function (err) {
                reject(err)
              })
          }
        })
        return res;
      }*/
    }
  }

</script>

<style scoped lang="less">
  @import "less/common.css";

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    header {
      background-color: #7d61f2;
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
      padding: 44px 0;
      box-sizing: border-box;
    }
  }
</style>
