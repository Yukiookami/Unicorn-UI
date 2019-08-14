<template>
  <div class="unicorn-counter-sec">
    <img @click="changeNum('sub')" src="./img/sub.svg" alt="">
    <span>{{num}}</span>
    <img @click="changeNum('add')" src="./img/add.svg" alt="">
  </div>
</template>

<script>
  export default {
    data () {
      return {
        num: 0
      }
    },
    methods: {
      changeNum (flag) {
        flag === 'add' ? this.num++ : this.num--
        this.num < 0 ? this.num = 0 : this.num 

        this.$emit('on-change', this.num)
      }
    }
  }
</script>

<style lang="scss" scoped>
.unicorn-counter-sec {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 56px;
  height: 32px;

  & span {
    color: #5e6ef7;
    font-size: 14px;
  }

  & img {
    cursor: pointer;
  }
}
</style>