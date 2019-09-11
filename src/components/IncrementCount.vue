<template>
  <div>
    <button @click="increment" >加</button>
    <input type="text" v-model="num">
  </div>

</template>

<script>
import {EventBus} from '../bus';
export default {
  name:'IncrementCount',
  data(){
    return{
      num:3,
      deg:60
    }
  },
  methods:{
     increment(){
       EventBus.$emit('incremented',{
         num:4,
         deg:60
       })
     }
  }
}
</script>

<style>

</style>
