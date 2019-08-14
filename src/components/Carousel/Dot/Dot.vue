<template>
  <div class="unicorn-dot-sec">
    <Dot-item @changeDot="changeSel" v-for="index in total" :key="index" :color="color"
    :index="index" :selNum="selNum"></Dot-item>
  </div>
</template>

<script>
  import DotItem from './DotItem'

  export default {
    name: 'Dot',
    props: {
      // 需要生成的点数
      total: {
        type: Number
      },
      // 点的颜色, 只接收default和white
      color: {
        type: String,
        default: 'default',
        validator (value) {
          return value === 'default' || value === 'white';
        }
      }
    },
    data () {
      return {
        selNum: 1
      }
    },
    methods: {
      changeSel (index) {
        this.selNum = index
      }
    },
    components: {
      DotItem
    }
  }
</script>

<style lang="scss" scoped>
.unicorn-dot-sec {
  display: flex;
  align-items: center;

  & div {
    margin: 0 5px
  }

  & :first-child {
    margin-left: 0;
  }

  & :last-child {
    margin-right: 0;
  }
}
</style>