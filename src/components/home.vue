<template>
  <div id="home">
    <div class="city-wrap">
      <city></city>
    </div>
    <div class="data-org">
      <p>数据来自：<a href="https://openweathermap.org" target="_blank">openWeatherMap</a></p>
    </div>
  </div>
</template>

<script>
  import cityCard from '@/components/cityCard'
  export  default {
    name: 'home',
    components: {
      'city': cityCard
    }
  }
</script>

<style scoped lang="less">
  #home {
    position: absolute;
    width: 100%;
    min-height: 100%;
    /*margin-top: 44px;*/
    background-color: #362460;
    text-align: center;
  }
  .city-wrap {
    height: 600px;
    overflow: hidden;
  }
  .city-card {
    margin-top: 66px;
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
