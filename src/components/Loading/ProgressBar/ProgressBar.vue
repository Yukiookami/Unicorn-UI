<template>
  <div class="unicorn-progress-sec">
    <div class="unicorn-done-box" v-if="fixValue === 100">
      <span>Done</span>
      <img src="./img/done.svg" alt="">
    </div>
    <span v-else>{{fixValue}}%</span>
    <progress class="unicorn-progress-bar" max="100" :value="fixValue"></progress>
  </div>
</template>

<script>
  export default {
    props: {
      /**
       * @param {Number} 值为0-100之间的数值
       */
      value: {
        type: Number,
        default: 0
      }
    },
    computed: {
      fixValue () {
        return this.value.toFixed(2) / 1
      }
    }
  }
</script>

<style lang="scss" scoped>
.unicorn-progress-sec {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  width: 200px;
  height: 27px;

  .unicorn-done-box {
    display: flex;
    justify-content: center;

    & img {
      margin-left: 2px;
    }
  }

  & span {
    color: #00C48C;
    font-size: 14px;
  }

  .unicorn-progress-bar{
    width: 200px;
    height: 8px;
    border-radius: 4px;
    // IE 10+
    color: #00C48C;
    // 火狐
    background-color: #D5F2EA; 
  }
  /* 表示总长度背景色  谷歌 */
  .unicorn-progress-bar::-webkit-progress-bar{     
    background-color: #D5F2EA;
    border-radius: 0.2rem;
  }
  /* 表示已完成进度背景色  谷歌 */
  .unicorn-progress-bar::-webkit-progress-value{
    background: #00C48C;
    border-radius: 0.2rem; 
  }

  /* 表示已完成进度背景色  火狐*/
  .unicorn-progress-bar::-moz-progress-bar{
    background-color:#00C48C;
  }
}
</style>