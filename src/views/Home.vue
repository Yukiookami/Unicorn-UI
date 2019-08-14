<template>
  <div class="home">
    <Page pages="101"></Page>
    <br>

    <Progress-bar :value="proValue"></Progress-bar>

    <br>

    <Ellipsis></Ellipsis>

    <br>

    <Rotate></Rotate>

    <br>

    <Steps :current="next"></Steps>
    <button @click="go">下一步(用于测试的睿智按钮)</button>

    <br>
    <br>

    <Dot :total="dotNum"></Dot>

    <br>

    <MapPin content="DD斩首"></MapPin>
    <MapPin style="margin-left: 5rem" content="DD斩首" direction="right"></MapPin>
    <MapPin content="DD斩首" direction="left"></MapPin>
    <MapPin style="margin-left: 10rem" content="DD斩首" size="large"></MapPin>
    <MapPin content="DD斩首" size="large" direction="left"></MapPin>
    <MapPin content="DD斩首" size="large" direction="right"></MapPin>
    <MapPin style="margin-left: 5rem" content="DD斩首" size="small"></MapPin>
    <MapPin content="DD斩首" size="small" direction="left"></MapPin>
    <MapPin content="DD斩首" size="small" direction="right"></MapPin>

    <br>
    
    <StarReview @on-change="getPoint"></StarReview>
    <span>{{point}}</span>

    <br>

    <Counter></Counter>

    <br>

    <Switch-button></Switch-button>
    <br>
    <Switch-button disabled="disabled"></Switch-button>

    <br>

    <Calendar></Calendar>
  </div>
</template>

<script>
// @ is an alias to /src
import Page from '@/components/Page/Page'
import ProgressBar from '@/components/Loading/ProgressBar/ProgressBar'
import Ellipsis from '@/components/Loading/Ellipsis/Ellipsis'
import Rotate from '../components/Loading/Rotate/Rotate'
import Steps from '../components/Steps/Steps' 
import Dot from '../components/Carousel/Dot/Dot'
import MapPin from '../components/MapPin/MapPin'
import StarReview from '../components/StarReview/StarReview'
import Counter from '../components/Counter/Counter'
import SwitchButton from '../components/SwitchButton/SwitchButton'
import Calendar from '../components/Calendar/Calendar'

export default {
  name: 'home',
  data () {
    return {
      proValue: 0,
      next: 1,
      dotNum: 5,
      point: 5
    }
  },
  mounted () {
    let time = setInterval(() => {
      if (parseInt(this.proValue) === 100) {
        this.proValue = 100
        clearInterval(time)
      } else {
        this.proValue += 0.1
      }
    }, 1);
  },
  methods: {
    // 测试步骤条
    go () {
      if (this.next < 4) {
        this.next++
      } else {
        this.next = 1
      }
    },
    // 测试星级评论on-change
    getPoint (point) {
      this.point = point
    }
  },
  components: {
    // 分页组件
    Page,
    // 进度条组件
    ProgressBar,
    // 动态省略号
    Ellipsis,
    // 旋转loading
    Rotate,
    // 步骤条
    Steps,
    // 轮播点
    Dot,
    // 聊天框
    MapPin,
    // 星级评分
    StarReview,
    // 数字加减
    Counter,
    // 开关
    SwitchButton,
    // 日历组件
    Calendar
  }
}
</script>

<style>
body {
  height: 500vh;
  background-color: rgba(0, 0, 0, .1);
}
</style>
