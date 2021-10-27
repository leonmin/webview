<template>
  <div id="list" class="list">
    <p>h5</p>
    <button @click="handleClick">按钮</button>
    <div></div>
    <button @click="handleDetail">详情</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      wx: null
    }
  },
  mounted () {
    this.wx = window.wx
  },
  methods: {
    handleClick () {
      this.wx.miniProgram.postMessage({
        data: {
          name: 'lily'
        }
      })
    },
    handleDetail () {
      this.wx.miniProgram.postMessage({
        data: {
          name: 'lily'
        }
      })
      this.wx.miniProgram.navigateTo({
        url: '/pages/detail/detail'
      })
    }
  }
}
</script>
<style scoped>
.list {
  width: 100%;
  height: 100vh;
  overflow-y: scroll;
  padding: 15px;
  box-sizing: border-box;
}
.item {
  width: 100%;
  height: 200px;
  background: #f3f3f3;
  margin-bottom: 15px;
}
#load {
  border-bottom: 1px solid #f5f5f5;
}
</style>
