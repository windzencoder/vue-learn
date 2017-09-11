<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{ msgfromfather }}</h1>
    <button v-on:click="onClickMe">Click!</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'hello from componmentA'
    }
  },
  //父组件向子组件传递的参数，注意以字符串的形式
  props:['msgfromfather'],
  methods:{
    onClickMe:function()
    {
      console.log(this.msgfromfather)
      //子组件触发事件,this.msg为传递的参数
      this.$emit('child-tell-me-something', this.msg)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
