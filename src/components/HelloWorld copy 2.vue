<template>
  <div id="list" class="list">
    <div class="item" v-for="(item) in list" :key="item.id">
      <div>{{item.name}}</div>
    </div>
    <div id="load"></div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      list: [],
      observer: null
    }
  },
  mounted () {
    this.list = Array.from({length: 20}, (o, i) => ({
      id: i + 1,
      name: 'item' + i
    }))
    this.observer = new IntersectionObserver(this.handleLoadMore, {
      root: document.querySelector('#list')
    })
    const view = document.querySelector('#load')
    this.observer.observe(view)
  },
  methods: {
    handleLoadMore () {
      const length = this.list.length
      const list = Array.from({length: 20}, (o, i) => ({
        id: length + i,
        name: `item${length + i}`
      }))
      this.handleQueue(list).then((res) => {
        this.list.push(...res)
      })
    },
    handleQueue (list) {
      const result = []
      return list.reduce((promise, item) => {
        return promise.then(() => {
          return this.handleWork(item).then((res) => {
            result.push(res)
          })
        })
      }, Promise.resolve()).then(() => {
        return result
      })
    },
    handleWork (item) {
      return new Promise(resolve => {
        setTimeout(() => {
          resolve(item)
        }, 0)
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
