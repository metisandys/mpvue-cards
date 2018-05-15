<template>
  <div class="left-slip-wrap">
    <div class="items">
      <div class="item" @touchstart="touchS" @touchmove="touchM" @touchend="touchE" :style="deleteSlider">
        <div class="txt">{{index}}</div>
      </div>
      <div class="remove" ref="remove">删除</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LeftSlip',
  data () {
    return {
      index: '嘻嘻哈哈',
      startX: 0, // 开始位置
      endX: 0,
      moveX: 0,
      disX: 0,
      deleteSlider: ''
    }
  },
  methods: {
    touchS (ev) {
      // console.log(ev)
      // tounches类数组，等于1时表示此时有只有一只手指在触摸屏幕
      if (ev.touches.length === 1) {
        // 记录开始位置
        this.startX = ev.touches[0].clientX
      }
    },
    touchM (ev) {
      // 获取删除按钮的宽度，此宽度为滑块左滑的最大距离.目前没用，没找到小程序控制节点的方法，先写死宽度了
      // const wd = this.$refs.remove.offsetWidth
      // const query = wx.createSelectorQuery()
      // const a = query.select('.remove').boundingClientRect()
      // console.log(a)
      const wd = 100 // 根据css先写死
      if (ev.touches.length === 1) {
        // 滑动时距离浏览器左侧实时距离
        this.moveX = ev.touches[0].clientX
        // 起始位置减去 实时的滑动的距离，得到手指实时偏移距离
        this.disX = this.startX - this.moveX
        // 如果是向右滑动或者不滑动，不改变滑块的位置
        if (this.disX < 0 || this.disX === 0) {
          this.deleteSlider = 'transform:translateX(0px)'
        // 大于0，表示左滑了，此时滑块开始滑动
        } else if (this.disX > 0) {
          // 具体滑动距离我取的是手指偏移距离*5。
          this.deleteSlider = 'transform:translateX(-' + this.disX * 5 + 'px)'
          // 最大也只能等于删除按钮宽度
          if (this.disX * 5 >= wd) {
            this.deleteSlider = 'transform:translateX(-' + wd + 'px)'
          }
        }
      }
    }
    // touchE (ev) {
    //   const wd = 100 // 同上个方法
    //   console.log(ev)
    //   if (ev.changedTouches.length === 1) {
    //     const endX = ev.changedTouches[0].clientX
    //     this.disX = this.startX - endX
    //     // 如果距离小于删除按钮一半,强行回到起点
    //     if ((this.disX * 5) < (wd / 2)) {
    //       this.deleteSlider = 'transform:translateX(0px)'
    //     } else {
    //       // 大于一半 滑动到最大值
    //       this.deleteSlider = 'transform:translateX(-' + wd + 'px)'
    //     }
    //   }
    // }
  }
}
</script>

<style lang="less">
.left-slip-wrap{
  height: 64px;
  width: 100%;
  margin: 0 auto;
  box-sizing: border-box; 
  .items{  
    width: 100%;
    height:100px;
    position: relative;
    user-select: none;
    .item{
      position: absolute;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      background:green;
      z-index: 100;
      //  设置过渡动画
      transition: 0.3s
    }
    .remove{
      position: absolute;
      width:100px;
      height:100px;
      background:red;
      right: 0;
      top: 0;
      color:#fff;
      text-align: center;
      font-size: 32px;
      line-height: 100px;
    }
    .item:last-child{
      border-bottom: 2rpx solid #eee;
    }
  }
}
</style>

