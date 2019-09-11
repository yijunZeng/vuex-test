<template>
<!-- 自定义事件的v-model使用 -->
<!-- VS自定义事件 -->
  <div>
    <p>我是儿子，父亲对我说： {{give}}</p>
    <p>我是儿子，我对父亲说：<button @click="returnBackFn">回应</button></p>
  </div>
</template>

<script>
export default {
  name:'BaseInput',
  props:{
    give:String
  },
  // v-model
  model:{
    prop:'give',
    event:'returnBack'
  },
  data(){
    return{

    }
  },
  methods:{
    returnBackFn(){
      this.$emit('returnBack','还你200块')
    }
  }
}
</script>

<style>

</style>
