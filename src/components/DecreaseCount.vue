<template>
  <button @click="decrease">减</button>
</template>

<script>
import {EventBus} from '../bus'
export default {
  name:"DecreaseCount",
  data(){
    return{
      num:2,
      deg: 180
    }
  },
  methods:{
    decrease() {
      EventBus.$emit('decreased',{
        num:2,
        deg:180
      })
    }
  }

}
</script>

<style>

</style>
