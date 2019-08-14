<template>
  <div @mouseleave="goback" class="unicorn-star-sec">
    <div v-for="index in 5" :key="index" class="unicorn-star">
      <img v-if="index !== point && index === point + 0.5" src="./img/star-half.svg" alt="半星">
      <img v-else-if="index > point" src="./img/star-no.svg" alt="无星">
      <img v-else-if="index <= point" src="./img/star-yes.svg" alt="满星">

      <div @mousemove="change('goHalf', index)" @click="getPoint()" class="unicorn-mask-left"></div>
      <div @mousemove="change('goFull', index)" @click="getPoint()" class="unicorn-mask-right"></div>
    </div>
  </div>
</template>

<script>
/**
 * 有个on-change方法，返回当前星级评分
 */
  export default {
    data () {
      return {
        point: 5,
        savePoint: 5,
        wantPoint: 5
      }
    },
    methods: {
      /**
       * @param {String} flag 接收一个字符串，来判断满星还是半星
       * @param {Number} index 接收一个数字，判断当前为第几颗星
       */
      change (flag, index) {
        index === 1 ? flag === 'goFull' ? this.point = index : this.point = 0
        : flag === 'goFull' ? this.point = index : this.point = index - 0.5

        this.wantPoint = this.point
        this.$emit('on-change', this.point)
      },
      /**
       * 鼠标离开时恢复原来评分
       */
      goback () {
        this.point = this.savePoint
        this.$emit('on-change', this.point)
      },
      /**
       * on-change函数，返回并保存当前评分
       */
      getPoint () {
        this.savePoint = this.wantPoint
        this.point = this.wantPoint
        this.$emit('on-change', this.point)
      }
    }
  }
</script>

<style lang="scss" scoped>
.unicorn-star-sec {
  display: flex;
  align-items: center;
  width: 110px;

  & :first-child {
    margin-left: 0 !important;
  }

  & :last-child {
    margin-right: 0 !important;
  }

  .unicorn-star {
    position: relative;
    margin: 0 5px;
    height: 14px;
    width: 14px;
    line-height: 0;
    cursor: pointer;

    .unicorn-mask-left,
    .unicorn-mask-right {
      position: absolute;
      height: 14px;
      width: 7px;
      top: 0;
    }

    .unicorn-mask-left {
      left: 0;
    }

    .unicorn-mask-right {
      right: 0;
    }
  }

}
</style>