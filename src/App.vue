<template>
  <div id="app">
   <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item.isFinished}"
          v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
    <p>child tells me :{{childwords}}</p>
    <componentA msgfromfather="hison!"
    v-on:child-tell-me-something="lisenToMyBoy"></componentA>
  </div>
</template>

<script>
  import Store from './store'
  import ComponentA from './components/componentA'
export default{
   data :function(){
       return {
         title:'this is a todo list',
         items:Store.fetch(),
//         items:[
//           {
//             label:'coading',
//             isFinished:false
//           },
//           {
//             label:'working',
//             isFinished:true
//           }
//         ],
         newItem:'',
         childwords:''
       }
     },
  components:{ ComponentA },
  watch:{
    items:{
      handler:function (items) {
        Store.save(items)
      },
      deep:true
    }

  },
  methods :{
    toggleFinish:function (item) {
//      console.log(item)
      item.isFinished = !item.isFinished
    },
    addNew :function () {
      this.items.push({
        label:this.newItem,
        isFinished:false
      })
//      console.log(this.newItem)
      this.newItem = ''
    },
    lisenToMyBoy : function (msg) {
      this.childwords = msg;
    }
  }
}
</script>

<style>
  .finished{
    text-decoration: underline;
  }
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
