<template>
  <div class="unicorn-steps-sec">
    <Step v-for="index in total" :key="index"
    :index="index" :current="current" :total="total"></Step>
  </div>
</template>

<script>
  import Step from './Step'

  export default {
    name: 'Steps',
    props: {
      // 当前进行到的步骤
      current: {
        type: Number,
        default: 4
      },
      // 一共有的步骤数
      total: {
        type: Number,
        default: 4
      }
    },
    components: {
      Step
    }
  }
</script>

<style lang="scss" scoped>
.unicorn-steps-sec {
  display: flex;
  align-items: center;
}
</style>