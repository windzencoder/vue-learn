<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{finished: item.isFinished}" 
      v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>

    <!-- 将驼峰法(camelCase)转换到短横线法(kebab-case) -->
    <componment-a msgfromfather='msg from father'></componment-a>

  </div>
</template>

<script>

import Store from './store'
import Hello from './components/Hello'
//导入子组件
import ComponmentA from './components/componmentA'
console.log(Store)

export default {

  name: 'app',
  components: {
    //记得要注册子组件
    Hello,ComponmentA
  },
  data:function(){
    return {
      title:"this is a todo list",
      //数据
      items:Store.fetch(),
      newItem: ''
    }
  },
  methods: {
    toggleFinish:function(item)
    {
      console.log(item.isFinished = !item.isFinished);
    },
    //按下enter，添加新项目
    addNew:function()
    {
      console.log(this.newItem)
      //添加到items中
      this.items.push({
        label:this.newItem,
        isFinished:false
      })
      this.newItem = ''
    }
  },
  //监测items的变化
  watch:{
    items:{
      handler: function (items) {
        //保存items
        Store.save(items)
      },
      deep: true
    }
  }
}
</script>

<style>
.finished
{
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
