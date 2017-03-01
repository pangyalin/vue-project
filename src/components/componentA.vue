<template>
  <div class="hello">
    <h1>{{msg}}</h1>
    <h2>{{msgfromfather}}</h2>
    <button v-on:click="onClickme">open mouse!</button>
  </div>
</template>

<script>

  export default{
    data :function(){
      return {
        msg:'hello from component a!'
      }
    },
    watch:{

    },
    props:['msgfromfather'],
//    子组件必须在props里注册 我接受这个属性
    methods : {
      onClickme:function () {
        console.log(this.msgfromfather)
        this.$emit('child-tell-me-something',this.msg);
      }
    }
  }
</script>

<style>

</style>
