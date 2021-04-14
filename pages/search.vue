<template>
  <div>
    123
    {{$store.state.todos.list}}
    <ul>
      <li v-for="(item,index) in list" :key="index">{{item}}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  layout: 'search',
  data() {
    return {
      list: []
    }
  },
  // 服务端的渲染是不执行mounted的
  // async mounted() {
  //   let {status, data: {list}} = await axios.get('/city/list')
  //   if (status === 200) {
  //     this.list = list
  //   }
  // }
  // ssr获取异步数据（页面没有闪动，很流畅）
  async asyncData() {
    let {status, data: {list}} = await axios.get('http://localhost:3000/city/list')
    if (status === 200) {
      return {
        list
      }
    }
  }
}
</script>

<style>
</style>
