<template>
<div>
  <div class="board">
    <a v-for="type in types" :key="type.id">
      <img :src="type.url" class="pics">
    </a>
  </div>
</div>
</template>

<script>
    export default {
      data(){
        return{
          types:[
            {
              id:1,
              url:"/static/img/7rm.png"
            },
            {
              id:2,
              url:"/static/img/30rm.png"
            },
            {
              id:3,
              url:"/static/img/lz.png"
            },
            {
              id:4,
              url:"/static/img/bq.png"
            },
            {
              id:5,
              url:"/static/img/dxt.png"
            }
          ]
        }
      },
        name: "Type"
    }
</script>

<style scoped>
  .board {
    margin-top: -4px;
    padding-bottom: 4px;
    min-height: 228px;
  }
  .pics{
    width: 280px;
    height: 50px;
  }
</style>
