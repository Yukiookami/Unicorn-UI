<template>
<!-- Page分页组件 -->
  <div class="page-sec" v-if="showAll">
    <div v-for="(number, index) in relPages" :key="index">
      <Page-item :pageNumber='number' :index='index'
      :clickNum="clickNum" @clicked="getPage"></Page-item>
    </div>
  </div>

  <div class="page-sec" v-else>
    <div @click="go('back')" class="margin-r img-box" :class="{'cont-use': !useL}">
      <div class="boom-box" :class="{'boom': showBoomL}"></div>
      <img src="./img/back.svg" alt="">
    </div>

    <div>
      <Page-item :index='pageList[showListPage].index' 
      :pageNumber='pageList[showListPage].pageNumber'
      @clicked="getPage" :clickNum="clickNum"></Page-item>
    </div>

    <!-- 没有到最后 -->
    <div v-if="!last">
      <Page-item :index='pageList[showListPage + 1].index' 
      :pageNumber='pageList[showListPage + 1].pageNumber'
      @clicked="getPage" :clickNum="clickNum"></Page-item>
    </div>

    <div v-if="!last">
      <Page-item show="..."></Page-item>
    </div>

    <!-- 到最后 -->
    <div v-if="last">
      <Page-item show="..."></Page-item>
    </div>
    
    <div v-if="last">
      <Page-item :index='pageList[relPages - 3].index' 
      :pageNumber='pageList[relPages - 3].pageNumber'
      @clicked="getPage" :clickNum="clickNum"></Page-item>
    </div>

    <div>
      <Page-item :index='pageList[relPages - 2].index' 
      :pageNumber='pageList[relPages - 2].pageNumber'
      @clicked="getPage" :clickNum="clickNum"></Page-item>
    </div>

    <div>
      <Page-item :index='pageList[relPages - 1].index' 
      :pageNumber='pageList[relPages - 1].pageNumber'
      @clicked="getPage" :clickNum="clickNum"></Page-item>
    </div>

    <div @click="go('go')" class="img-box" :class="{'cont-use': !useR}">
      <div class="boom-box" :class="{'boom': showBoomR}"></div>
      <img src="./img/go.svg" alt="">
    </div>
  </div>
</template>

<script>
import PageItem from './PageItem'
import './css/boom.css'

export default {
  /**
   * 接收2个参数
   * @param {String} pages 为总条数 默认值1
   * @param {String} pageSize 为每一页的条数 默认值10
   */
  props: {
    pages: {
      type: String,
      default: '1'
    },
    pageSize: {
      type: String,
      default: '10'
    }
  },
  data () {
    return {
      // 多页隐藏
      showAll: true,
      // 点击页面
      clickNum: 0,
      // 页面数组
      pageList: [],
      // 控制前两个页面的显示
      showListPage: 0,
      // 变换显示方式
      last: false,
      // 控制翻页按钮特效显现
      showBoomL: false,
      showBoomR: false,
      // 控制按钮禁用
      useL: false,
      useR: true
    }
  },
  computed: {
    // 计算出页数
    relPages () {
      return Math.ceil(+this.pages / +this.pageSize)
    }
  },
  mounted () {
    if(this.relPages > 5) {
      this.showAll = false
      for (let i = 0; i < this.relPages; i++) {
        this.pageList.push({
          index: i,
          pageNumber: i + 1
        })
      }
    }
  },
  methods: {
    // 更改选中状态，并且在组件外使用 on-change 事件可以获得当前被点击页数
    getPage (pageNumber) {
      this.$emit('on-change', pageNumber)
      this.clickNum =  --pageNumber

      let soui = this.clickNum - this.showListPage

      if(soui === 1) {
        this.showListPage = this.clickNum
      }

      if (pageNumber === 0) {
        this.last = false
        this.useL = false
        this.useR = true
      }

      if (pageNumber === this.relPages - 1) {
        this.useR = false
        this.useL = true
      } 

      if (pageNumber !== 0 && pageNumber !== this.relPages - 1) {
        this.useR = true
        this.useL = true
      }

      if (pageNumber >= this.relPages - 3) {
        this.showListPage = 0
        this.last = true
      }
    },
    // 按钮控制前进后退
    go (flag) {
      if (flag === 'go') {
        this.useR = true
        this.useL = true
        this.showBoomR = true
        setTimeout(() => {
          this.showBoomR = false
        }, 300)
        if (this.clickNum !== this.relPages - 1) {
          this.clickNum++
        }

        if (this.clickNum === this.relPages - 1) {
          this.useR = false
        }
      } else {
        this.useL = true
        this.useR = true
        this.showBoomL = true
        setTimeout(() => {
          this.showBoomL = false
        }, 300)
        if (this.clickNum !== 0) {
          this.clickNum--
        }

        if (this.clickNum === 0) {
          this.useL = false
        }
      }
  
      if (this.clickNum >= this.relPages - 3) {
        this.showListPage = 0
        this.last = true
      } else {
        if (this.clickNum <= this.relPages - 3) {
          this.showListPage = this.clickNum
          this.last = false
        }
      }
    }
  },
  components: {
    PageItem
  }
}
</script>

<style lang="scss" scoped>
.page-sec {
  display: flex;
  align-items: center;

  & :last-child div{
    margin-right: 0;
  }

  .img-box {
    display: flex;
    align-items: center;
    position: relative;
    height: 26px;
    width: 16px;
    cursor: pointer;

    .boom-box {
      position: absolute;
      left: 30%;
    }

    & img {
      width: 100%;
    }

  }

  .cont-use {
    filter: grayscale(100%);
    cursor: not-allowed;
  }

  .margin-r {
    margin-right: 10px;
  }

  .margin-l {
    margin-left: 10px;
  }
}
</style>
