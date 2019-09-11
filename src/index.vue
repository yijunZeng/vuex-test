<template>
    <div>
        <!-- 检验EventsBus的$on  $emit事件 -->
        <Decrease/>
        <Increment ref="incre"/>
        <p>fontCount:{{fontCount}}</p>
        <button @click="plus">+++</button><span>backCount:{{backCount}}</span>
        <p>fontCount:{{fontCount}}</p>
        <button @click="decre">---</button><span>backCount:{{backCount}}</span>
        <!-- Vue的ref使用 -->
        <input type="text" ref="msgText" v-model="msg">
        <button @click="getElement" ref="btn">getElement</button>
        <!-- 自定义事件的v-model使用--自定义事件 -->
        <p>我是父亲，我对儿子说：{{giveChild}}</p>
        <Baseinput @returnBack='returnBacks' :give="giveChild"></Baseinput>
        <p>我是父亲，我对儿子说：<button @click="returnBackAgain">我不要了，给回你</button></p>
        <p>=====================================</p>
        <!-- 自定义事件的v-model使用--自定义v-model -->
        <p>我是父亲，我对儿子说：{{giveChild}}</p>
        <Baseinput v-model="giveChild"></Baseinput>
    </div>

</template>

<script>
// props的传递都是单向的，最好不修改
import CommonButton from '@/components/common';
import Baseinput from './components/BaseInput';
import Decrease from './components/DecreaseCount';
import Increment from './components/IncrementCount';
import { EventBus } from './bus';
export default {

    data(){
        return{
          searchInput:'',
          fontCount:0,
          backCount:0,
          degValue:0,
          msg:'11',
          giveChild:'我给你100块'
        }
    },
    components:{CommonButton,Baseinput,Decrease,Increment},
    beforeMount(){
      // console.log("beforeMount"+ this.$refs.msgText.value);
      // console.log("beforeMount"+ this.$refs);
    },
    mounted(){
      /**
       * 检验EventsBus的$on  $emit事件
       */
      // EventBus.$on('incremented',({num,deg})=>{
      //   this.fontCount += num
      //   console.log("fontCount",this.fontCount);
      //   this.$nextTick(()=>{
      //     this.backCount += num
      //     this.degValue += deg
      //   })
      // });
      // EventBus.$on('decreased',({num,deg})=>{
      //   this.fontCount -= num
      //   console.log("fontCount",this.fontCount);
      //   this.backCount -= num
      //     this.degValue -= deg
      //   // this.$nextTick(()=>{
      //   //   this.backCount -= num
      //   //   this.degValue -= deg
      //   // })
      // })
      // Vue的ref使用
      console.log("Mounted"+ this.$refs.msgText.value);
    },
    methods:{
      plus () {
        // 接收和分发的问题
        EventBus.$on('incremented',({num,deg})=>{
          this.fontCount += num
          console.log("fontCount",this.fontCount);
          this.$nextTick(()=>{
            this.backCount += num
            this.degValue += deg
          })
        });
      },
      decre () {
         EventBus.$on('decreased',({num,deg})=>{
          this.fontCount -= num
          console.log("fontCount",this.fontCount);
          this.backCount -= num
            this.degValue -= deg
          this.$nextTick(()=>{
            this.backCount -= num
            this.degValue -= deg
          })
        })
      },
      getElement(){
        // console.log('getElement'+ JSON.stringify(this.$refs));
        // console.log("Mounted"+ this.$refs.incre.increment());

      },
      // 可以同名
      returnBacks(val){
        this.giveChild = val
      },
      returnBackAgain (){
        this.giveChild= '把200给回给你'
      }
    }

}
</script>

<style>

</style>
