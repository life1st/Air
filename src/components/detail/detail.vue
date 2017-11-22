<template>
  <div class="detail-wrap">
    <div class="now-detail">
      <div class="img-wrap">
        <img src="../../img/detail/sunny.png" alt="weather-img">
      </div>
      <div class="content">
        <h2>cityName</h2>
        <p>Sunny 19°</p>
      </div>
    </div>
    <div class="timeline" >
      <div class="time-item" v-for="item in items">
        <div class="date">
          <p>morning</p>
          <p>12:00</p>
        </div>
        <div class="weather-img">
          <img src="" alt="">
        </div>
        <div class="detail">
          <p>Sunny</p>
          <p>19℃</p>
          <div class="info">
            <div class="wind">
              <div class="img-wrap">
                <img src="" alt="">
              </div>
              <p>4mph</p>
            </div>
            <div class="humidity">
              <div class="img-wrap">

              </div>
              <p>63%</p>
            </div>
            <div class="rainy-chance">
              <div class="img-wrap">
                <img src="" alt="">
              </div>
              <p>14%</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>
<script>
  export default {
    data() {
      return {
        items: {

        }
      }
    },
    methods: {
      toData: function () {
        new Promise((resolve,reject) => {

        })
      }
    }
  }
</script>
<style scoped lang="less">
  .now-detail {
    background-color: #69bcf7;
    width: 100%;
    height: 190px;
  }
  .img-wrap {
    width: 100px;
    height: 100px;
    img {
      width: 100%;
    }
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
