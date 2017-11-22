<template>
    <div class="city-card">
      <p class="temperature">{{info.temperature}}</p>
      <p class="city-name">{{info.cityName}}</p>
      <div class="status">
        <img src="../img/rainy-icon.png" alt="rainy">
        <span>{{info.status}}</span>
      </div>
      <div class="detail">
        <div class="wind">
          <img src="../img/wind-icon.png" alt="">
          <p class="num">{{info.windSpeed}}</p>
          <p class="chance">Deg:{{info.deg}}</p>
        </div>
        <div class="rainy">
          <img src="../img/rainyChance-icon.png" alt="">
          <p class="num">{{info.rainyChance}}</p>
          <p class="chance">CHANCE</p>
        </div>
        <div class="humidity">
          <img src="../img/humidity-icon.png" alt="">
          <p class="num">{{info.humidity}}</p>
          <p class="chance">HUMIDITY</p>
        </div>
      </div>
      <div class="weekly">
        <div class="day">
          <p>TUE</p>
          <div class="img-wrap">
            <img src="../img/tue-icon.png" alt="">
          </div>
          <p class="c-temperature">12</p>
        </div>
        <div class="day">
          <p>WED</p>
          <div class="img-wrap">
          <img src="../img/wed-icon.png" alt="">
          </div>
            <p class="c-temperature">8</p>
        </div>
        <div class="day">
          <p>THU</p>
          <div class="img-wrap">
          <img src="../img/thu-icon.png" alt="">
          </div>
            <p class="c-temperature">6</p>
        </div>
        <div class="day">
          <p>FRI</p>
          <div class="img-wrap">
          <img src="../img/fri-icon.png" alt="">
          </div>
            <p class="c-temperature">9</p>
        </div>
        <div class="day">
          <p>SAT</p>
          <div class="img-wrap">
          <img src="../img/sat-icon.png" alt="">
          </div>
            <p class="c-temperature">4</p>
        </div>
        <div class="day">
          <p>SUN</p>
          <div class="img-wrap">
          <img src="../img/sun-icon.png" alt="">
          </div>
            <p class="c-temperature">-3</p>
        </div>
      </div>
    </div>
</template>
<script>
  import jsonp from 'jsonp'
  import axios from 'axios'
  export default {
    data() {
      return {
        info: {
          temperature: 23,
          cityName: 'San Francisco',
          status: 'Rainy',
          windSpeed: 8,
          rainyChance: 23,
          humidity: 83,
          deg: 0
        }
      }
    },
    mounted() {
      var _this = this
      this.toData()
        .then(function (res) {
          console.log(res)
          var res = res.data
          var info = _this.info
          info.cityName = res.city.name
          info.temperature = parseInt(res.list[0].main.temp)
          info.windSpeed = res.list[0].wind.speed
          info.rainyChance = res.list[0].rain['3h']*100 || '0'
          info.status = res.list[0].weather[0].description
          info.humidity = res.list[0].main.humidity
          info.deg = Math.floor(res.list[0].wind.deg)
        })
        .catch(function (err) {
          console.log(err)
        })
    },
    methods: {
      toData: function () {
        var weatherData = new Promise((resolve,reject) => {
          if (localStorage.getItem('time') &&
            new Date().getTime() - localStorage.getItem('time') < 6000000){
            console.log('old weather data')
            resolve(JSON.parse(localStorage.getItem('weatherData')))
          }else {
            localStorage.setItem('time', new Date().getTime())
            console.log('new weather data')
//            var url = 'http://restapi.amap.com/v3/ip'
            var amapKey = 'a75aef737f1db811578d960310aba54e'
            var url = 'http://apis.map.qq.com/ws/location/v1/ip'
            var qqKey = 'CSIBZ-4LKWV-HNIPZ-UYVZG-BYG6O-PSBMP'
            var urls = url + '?&key=' + qqKey + '&output=jsonp'

            var resWeatherData = new Promise((resolve,reject) => {
              jsonp(urls, null, function (err, data) {
                if (err){
                  reject(err)
                }
                resolve(data)
              })
            }).then((res) => {
              localStorage.setItem('city',JSON.stringify(res))
              var loc = {
                lat: 30.66667,
                lon: 104.066673 //默认地点坐标,随便写的，城市是成都
              }
              var location = res.result.location
              console.log(location,'loc')
              loc.lon = location.lng
              loc.lat = location.lat
              var url = 'http://api.openweathermap.org/data/2.5/forecast'
              var oWMKey = '754faa9db2ccd9149d4b67acc25aa327'
              axios.get(url, {
                params: {
                  lat: loc.lat,
                  lon: loc.lon,
                  APPID: oWMKey,
                  lang: 'zh_cn',
                  units: 'metric'
                }
              }).then(function (res) {
                localStorage.setItem('weatherData',JSON.stringify(res))
                resolve(res);
              }).catch(function (err) {
                reject(err)
              })
            })
          }
        })
        return weatherData;
      },
    },
  }
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
      display: flex;
      justify-content: space-around;
      .day {
        margin-top: 26px;
      }
      .img-wrap {
        height: 20px;
        margin-top: 15px;
      }
      .c-temperature {
        font-size: 20px;
        line-height: 20px;
        margin-top: 8px;
        position: relative;
        &:after {
          content: '°';
          position: absolute;
          top: 0;
        }
      }
    }
  }
</style>
