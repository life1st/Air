<template>
  <div id="home">
      <div class="city-wrap">
        <city @click=""></city>
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
        refreshDate: Math.floor((new Date().getTime() - localStorage.getItem('time'))/(1000*60))
      }
    },
  }
</script>

<style scoped lang="less">
  #home {
    position: absolute;
    width: 100%;
    min-height: 100%;
    background-color: #362460;
    text-align: center;
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
