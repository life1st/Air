<template>
  <div class="timeline" >
    <div class="time-item" v-for="item in items">
      <div class="date">
        <p>{{item.dt_txt.split(' ')[0]}}</p>
        <p>{{item.dt_txt.split(' ')[1].split(':')[0]}}:00</p>
      </div>
      <div class="weather-img">
        <img src="" alt="">
      </div>
      <div class="detail">
        <p>{{item.weather[0].description}}</p>
        <p>{{Math.floor(item.main.temp)}}℃</p>
        <div class="info">
          <div class="wind">
            <div class="img-wrap">
              <img src="" alt="">
            </div>
            <p>{{item.wind.speed}}mph</p>
          </div>
          <div class="humidity">
            <div class="img-wrap">
              <img src="" alt="">
            </div>
            <p>{{Math.floor(item.rain['3h']*100)}}%</p>
          </div>
          <div class="rainy-chance">
            <div class="img-wrap">
              <img src="" alt="">
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
      })
    },
    methods: {

    }
  }
</script>
<style scoped lang="less">
  .timeline {
    background-color: #1a2432;
    color: #fff;
  }
  .time-item {
    height: 100px;
    .date,.weather-img,.detail {
      display: inline-block;
      font-size: 0;
      &>*{
        font-size: 14px;
      }
    }
    .detail {
      .info {
        .wind,.humidity,.rainy-chance {
          display: inline-block;
          font-size: 0;
          &>* {
            font-size: 14px;
          }
        }
      }
    }
  }
</style>
