<template>
  <div @click="click" class="page-item cup" :class="{'selected': clickNum === index}">
    <span class="cud" v-if="show">{{show}}</span>
    <span v-else>{{pageNumber}}</span>
  </div>
</template>

<script>
  export default {
    /**
     * @param {Number} pageNumber 无默认值，用于确认选取状态和返回当前页数
     * @param {Number} index 列表索引
     * @param {Number} clickNum 默认值1，用于渲染选中
     * @param {String} show 默认值无，显示指定字符串
     */
    props: {
      pageNumber: {
        type: Number
      },
      index: {
        type: Number
      },
      clickNum: {
        type: Number,
        default: 0
      },
      show: {
        type: String
      }
    },
    methods: {
      // 返回被点击的页数
      click () {
        this.$emit('clicked', this.pageNumber)
      }
    }
  }
</script>

<style lang="scss" scoped>
* {
  font-size: 14px;
}

.page-item {
  padding: .3rem .65rem;
  margin-right: .25rem;
  border-radius: 8px;
  color: #6979F8;
  transition: all .3s ease-in-out;
}

.cup {
  cursor: pointer;
}

.cud {
  cursor: default;
}

.selected {
  background-color: #6979F8;
  color: #FFF;
}
</style>