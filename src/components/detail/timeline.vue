<template>
  <div class="timeline" >
    <div class="time-item" v-for="item in items">
      <div class="date">
        <p>{{item.dt_txt.split(' ')[0].split('-')[1]}}月{{item.dt_txt.split(' ')[0].split('-')[2]}}日</p>
        <p>{{item.dt_txt.split(' ')[1].split(':')[0]}}:00</p>
      </div>
      <div class="weather-img">
        <img src="../../img/rainy-icon.png" alt="">
      </div>
      <div class="detail">
        <p>{{item.weather[0].description}}</p>
        <p>{{Math.floor(item.main.temp)}}℃</p>
        <div class="info">
          <div class="wind">
            <div class="img-wrap">
              <!--<img src="../../img/detail/timeline/icon1.png" alt="icon1">-->
            </div>
            <p>{{item.wind.speed}}mph</p>
          </div>
          <div class="humidity">
            <div class="img-wrap">
              <!--<img src="../../img/detail/timeline/icon2.png" alt="icon2">-->
            </div>
            <p v-if="item.rain">{{Math.floor(item.rain['3h']*100)}}%</p>
            <p v-else>0%</p>
          </div>
          <div class="rainy-chance">
            <div class="img-wrap">
              <!--<img src="../../img/detail/timeline/icon3.png" alt="icon3">-->
            </div>
            <p>{{item.main.humidity}}%</p>
          </div>
        </div>
      </div>
    </div>
    <div class="no-data" v-if="!this.items">
      <p>no-data</p>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'timeline',
    data() {
      return {
        items: [],
      }
    },
    mounted() {
      new Promise((resolve,reject) => {
        resolve(localStorage.getItem('weatherData'))
      }).then((data) => {
        var list = JSON.parse(data).data.list
        this.items = list
        console.log(list)
      })
    },
    methods: {

    }
  }
</script>
<style lang="less">
  .timeline {
    background-color: #1a2432;
    color: #fff;
    .date {
      vertical-align: top;
      text-align: right;
    }
    .weather-img {
      width: 65px;
      height: 100%;
      position: relative;
      vertical-align: top;
      img {
        position: relative;
        width: 40px;
        margin: 0 12px;
        display: inline-block;
        text-align: center;
        z-index: 10;
      }
      &:before {
        content: '';
        position: absolute;
        top: 0;
        bottom: 0;
        left: 50%;
        transform: translateX(-50%);
        z-index: 1;
        display: block;
        width: 4px;
        background-color: #2a3342;
      }
    }
  }
  .time-item {
    height: 100px;
    .date,.weather-img,.detail {
      padding-top: 23px;
      display: inline-block;
      font-size: 0;
      box-sizing: border-box;
      &>*{
        font-size: 14px;
      }
    }
    .detail {
      width: 50%;
      .info {
        padding-top: 6px;
        .wind,.humidity,.rainy-chance {
          display: inline-block;
          width: 30%;
          font-size: 0;
          &>* {
            font-size: 14px;
          }
        }
      }
      img {
        height: 10px;
      }
    }
  }
</style>
