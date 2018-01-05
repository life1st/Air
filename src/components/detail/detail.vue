<template>
  <div class="detail-wrap">
    <div class="now-detail">
      <div class="img-wrap">
        <!--<img src="../../img/detail/sunny.png" alt="weather-img">-->
      </div>
      <div class="content">
        <h2>{{content.citiName}}</h2>
        <h1>{{content.country}}</h1>
        <p>{{content.weather}} {{content.temp}}℃</p>
      </div>
    </div>
    <timeline></timeline>
  </div>
</template>
<script>
  import timeline from '@/components/detail/timeline'

  export default {
    components: {
      'timeline': timeline
    },
    data() {
      return {
        content: {
          citiName: '',
          country: '',
          weather: '',
          temp: ''
        }
      }
    },
    mounted() {
      new Promise((resolve,reject) => {
        resolve(localStorage.getItem('weatherData'))
      }).then((res) => {
        var data = JSON.parse(res).data
        console.log(data)
        this.content.citiName = data.city.name
        this.content.country = data.city.country
        this.content.weather = data.list[0].weather[0].description
        this.content.temp = Math.floor(data.list[0].main.temp)
      })
    }

  }
</script>
<style scoped lang="less">
  .now-detail {
    background-color: #69bcf7;
    width: 100%;
    height: 190px;
    border-bottom: 3px solid #fff;
    .img-wrap {
      width: 100px;
      height: 100px;
      margin: 38px 0 0 40px;
      float: left;
      img {
        width: 100%;
      }
    }
    .content {
      float: right;
      margin: 38px;
      h2,p {
        line-height: 26px;
        color: #fff;
        font-size: 16px;
      }
    }
  }

  .timeline {
    background-color: #1a2432;
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
