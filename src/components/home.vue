<template>
  <div id="home">
    <city></city>
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
    height: 100%;
    margin-top: -44px;
    background-color: #362460;
  }
  .city-card {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
  }
</style>
