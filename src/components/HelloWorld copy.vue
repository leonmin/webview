<template>
  <div>
    <div>
      {{content}}
    </div>
    <button @click="handleScan">扫码</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      content: ''
    }
  },
  methods: {
    handleScan () {
      window.wx.miniProgram.postMessage({
        data: {
          age: 25
        }
      })
      window.wx.miniProgram.reLaunch()
      // window.wx.scanQRCode({
      //   desc: 'scan',
      //   needResult: 1,
      //   scanType: ['qrCode'],
      //   success: (res) => {
      //     this.content = res
      //   },
      //   error: (err) => {
      //     this.content = err
      //   }
      // })
    }
  }
}
</script>

<style>

</style>
