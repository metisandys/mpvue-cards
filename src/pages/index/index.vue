<template>
  <div class="cards-list-wrap">
    <div class="list-item" v-for="(item, index) in list" :key="index">
      <LeftSlip :itemInfo="item"></LeftSlip>
    </div>
  </div>
</template>

<script>
import LeftSlip from '@/components/leftSlip'

export default {
  data () {
    return {
      list: [
        {
          text: '嘻嘻哈哈'
        },
        {
          text: '呵呵嘻嘻'
        },
        {
          text: '哈哈呵呵'
        }
      ]
    }
  },

  components: {
    LeftSlip
  },

  methods: {
    // bindViewTap () {
    //   const url = '../logs/main'
    //   wx.navigateTo({ url })
    // },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    }
    // clickHandle (msg, ev) {
    //   console.log('clickHandle:', msg, ev)
    // }
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>

<style lang="less">
.cards-list-wrap{
  .list-item{
    border-bottom: 1px solid #cccccc;
  }
}
</style>
