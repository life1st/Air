<template>
    <div class="city-card">
      <p class="temperature">{{temperature}}</p>
      <p class="city-name">{{cityName}}</p>
      <div class="status">
        <img src="../img/rainy-icon.png" alt="rainy">
        <span>{{status}}</span>
      </div>
      <div class="detail">
        <div class="wind">
          <img src="../img/wind-icon.png" alt="">
          <p class="num">{{windSpeed}}</p>
          <p class="chance">CHANCE</p>
        </div>
        <div class="rainy">
          <img src="../img/rainyChance-icon.png" alt="">
          <p class="num">{{rainyChance}}</p>
          <p class="chance">CHANCE</p>
        </div>
        <div class="humidity">
          <img src="../img/humidity-icon.png" alt="">
          <p class="num">{{humidity}}</p>
          <p class="chance">HUMIDITY</p>
        </div>
      </div>
      <div class="weekly">

      </div>
    </div>
</template>
<script>
  import jsonp from 'jsonp'
  export default {

    data: function () {
      return {
        temperature: 23,
        cityName: 'San Francisco',
        status: 'Rainy',
        windSpeed: 8,
        rainyChance: 23,
        humidity: 83
      }
    }
  }

  jsonp('https://api.caiyunapp.com/v2/TAkhjf8d1nlSlspN/121.6544,25.1552/realtime.jsonp',null,function (err,data) {
    if (err){
      console.log(err)
    }else {
      console.log(data)
    }
  })
</script>
<style scoped lang="less">
  .city-card {
    width: 300px;
    height: 500px;
    text-align: center;
    box-shadow: 1px 1px 5px #534485;
    border-radius: 8px;
    color: #fff;
    background: url("../img/card-bg.png") center no-repeat;
    .temperature {
      font-size: 80px;
      line-height: 80px;
      margin-top: 74px;
      position: relative;
      &:after {
        content: '°';
        position: absolute;
      }
    }
    .city-name {
      font-size: 22px;
      line-height: 22px;
      margin-top: 20px;
    }
    .status {
      margin-top: 22px;
      img {
        vertical-align: sub;
      }
      span {
        font-size: 20px;
        line-height: 20px;
      }
    }
    .detail {
      margin-top: 42px;
      display: flex;
      justify-content: space-around;
      img {
        height: 18px;
      }
    }
    .chance {
      font-size: 10px;
    }
    .num {
      font-size: 27px;
      line-height: 27px;
      position: relative;
      &:after {
        position: absolute;
        top: 0;
        font-size: 10px;
        line-height: 10px;
        transform: scale(.8);
      }
    }
    .wind {
      position: relative;
      .num:after {
        content: 'MPH';
      }
    }
    .rainy {
      .num:after {
        content: '%';
      }
    }
    .humidity {

    }
    .weekly {
      height: 120px;
      width: 100%;
      position: absolute;
      bottom: 0;
      left: 0;
      background-color: rgba(0,0,0,0.3);
      border-radius: 0 0 8px 8px;
    }
  }
</style>
