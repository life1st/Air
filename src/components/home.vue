<template>
  <div id="home">
      <div class="city-wrap">
        <router-link to="/detail">
          <city></city>
        </router-link>
      </div>
      <div class="data-org">
        <p>数据来自：
          <a href="https://openweathermap.org" target="_blank">openWeatherMap</a>
        {{refreshDate}}分钟前更新
        </p>
      </div>
    </div>
</template>

<script>
  import cityCard from '@/components/cityCard'
  export  default {
    name: 'home',
    components: {
      'city': cityCard
    },
    data() {
      return {
        refreshDate: 0
      }
    },
    mounted() {
      new Promise((resolve,reject) => {
        resolve(localStorage.getItem('time'))
      }).then((time) => {
        console.log(time)
        this.refreshDate = Math.floor((new Date().getTime() - time)/(1000*60))
      })
    }
  }
</script>

<style scoped lang="less">
  #home {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    min-height: 100%;
    background-color: #362460;
    text-align: center;
    box-sizing: border-box;
    padding: 44px 0;
  }
  .city-wrap {
    width: 100%;
    height: 90%;
  }
  .city-card {
    margin-top: 26px;
    display: inline-block;
    position: relative;
  }
  .data-org {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
    color: #7c53dd;
    text-align: center;
    font-size: 10px;
    a {
      color: #fff;
    }
  }
</style>
