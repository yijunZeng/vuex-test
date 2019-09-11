<template>
  <div><button v-on:click="count++">{{buttonName}}++You clicked me {{ count }} times.</button></div>
</template>

<script>
export default {
  props:{
    buttonName:[String]
    },
    // props:['buttonName'],另外一个写法，不规定类型
  data(){

    return{
      count:1,

    }
  }
}
</script>

<style>

</style>
