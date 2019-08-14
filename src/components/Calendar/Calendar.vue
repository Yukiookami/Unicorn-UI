<template>
  <div class="unicorn-calendar-main">
    <div class="unicorn-calendar-sec">
      <div>
        <span>{{day}}</span>/<span>{{month}}</span>/<span>{{year}}</span>
      </div>

      <img v-if="!show" @click="getDateMoble(), showDay()" src="./img/calendar.svg" alt="">
      <img v-else @click="getDateMoble(), showDay()" src="./img/calendar-sel.svg" alt="">
    </div>

    <div v-show="show" class="unicorn-calendar-choose-sec">
      <div class="unicorn-calendar-choose-month">
        <img @click="changeMonth('back')" src="./img/back.svg" alt="上个月">
        <span>{{monthName[month / 1 - 1]}} {{year}}</span>
        <img @click="changeMonth('go')" src="./img/next.svg" alt="下个月">
      </div>

      <div class="unicorn-calendar-choose-day-sec">
        <div class="unicorn-calendar-choose-dayName">
          <span v-for="(item, index) in dayName" :key="index">{{item}}</span>
        </div>

        <div class="unicorn-line">
          <div v-for="index in 20" :key="index" class="unicorn-line-item"></div>
        </div>

        <!-- 具体天数列表 -->
        <div class="unicorn-day-sec">
          <div class="unicorn-dayLine">
            <span ref="dayLine0" v-for="index in 7" :key="index" 
            class="unicorn-day"
            :class="{'unicorn-day-notnow': index - 6 <= firstWeekday, 
            'unicorn-nowDate': index - firstWeekday - 6 === day}"
            @click="returnDay(index, 'first')">1</span>
          </div>

          <div class="unicorn-dayLine">
            <span ref="dayLine1" v-for="index in 7" :key="index" 
            class="unicorn-day"
            :class="{'unicorn-day-notnow': index < firstWeekday, 
            'unicorn-nowDate': index - firstWeekday + 1 === day}"
            @click="returnDay(index)">1</span>
          </div>
          
          <div class="unicorn-dayLine">
            <span ref="dayLine2" v-for="index in 7" :key="index" 
            class="unicorn-day"
            :class="{'unicorn-nowDate': index + 8 - firstWeekday === day}"
            @click="returnDay(index + 7)">1</span>
          </div>

          <div class="unicorn-dayLine">
            <span ref="dayLine3" v-for="index in 7" :key="index" 
            class="unicorn-day"
            :class="{'unicorn-nowDate': index + 15 - firstWeekday === day}"
            @click="returnDay(index + 14)">1</span>
          </div>

          <div class="unicorn-dayLine">
            <span ref="dayLine4" v-for="index in 7" :key="index" 
            class="unicorn-day"
            :class="{'unicorn-nowDate': index + 22 - firstWeekday === day}"
            @click="returnDay(index + 21)">1</span>
          </div>

          <div class="unicorn-dayLine">
            <span ref="dayLine5" v-for="index in 7" :key="index"
            class="unicorn-day"
            :class="{'unicorn-day-notnow': index > lastWeekday + 1,
            'unicorn-nowDate': index + 29 - firstWeekday === day}"
            @click="returnDay(index + 28)">1</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'calendar',
    data () {
      return {
        // 今年
        year: 1970,
        // 月数
        month: 1,
        // 今天号数
        day: 1,
        show: false,
        monthName: ['January', 'February', 'March', 
        'April', 'May', 'June', 'July', 'August', 
        'September', 'October', 'November', 'December'],
        dayName: ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT'],
        // 这个月的天数
        dayArrNow: [],
        // 下个月的天数
        dayArrAfter: [],
        // 上个月的天数
        dayArrBefore: [],
        // 今天的星期
        nowWeekday: 4,
        // 每个月第一天的星期数
        firstWeekday: 4,
        // 每个月最后一天的星期数
        lastWeekday: 6,
        isLeap: false
      }
    },
    methods: {
      getDateMoble () {
        this.show = !this.show
      },
      setDay (dayNum, arr) {
        for (let i = 1; i <= dayNum; i++) {
          arr.push(i)
        }
      },
      /**
       * 根据当月份生成日期
       * @param {Number} 当前月份
       * @param {Arr} 存储日期的数组
       */
      getDate (month, arr) {
        arr.splice(0)

        if (month === 1 || month === 3 || month === 5 
        || month === 7 || month === 8 || month === 10 
        || month === 12) {
          this.setDay(31, arr)
        } else if (month === 2) {
          if (this.isLeap) {
            this.setDay(29, arr)
          } else {
            this.setDay(28, arr)
          }
        } else {
          this.setDay(30, arr)
        }
      },
      // 生成当前以及上个月下个月的
      getDateNow () {
        let now = this.month / 1
        let after = now + 1
        let before = now - 1

        after > 12 ? after = 1 : after
        before < 1 ? before = 12 : before 

        if (this.year % 400 === 0 || (this.year % 4 === 0 && this.year % 100 !==  0)) {
          this.isLeap = true
        } else {
          this.isLeap = false
        }

        this.getDate(now, this.dayArrNow)
        this.getDate(after, this.dayArrAfter)
        this.getDate(before, this.dayArrBefore)
      },
      // 渲染日期
      showDay () {
        let dayIndex = 0

        // 日期dom
        let dayLine0 = this.$refs.dayLine0
        let dayLine1 = this.$refs.dayLine1
        let dayLine2 = this.$refs.dayLine2
        let dayLine3 = this.$refs.dayLine3
        let dayLine4 = this.$refs.dayLine4
        let dayLine5 = this.$refs.dayLine5

        // 渲染上个月的残留日期
        dayLine1.forEach((ele, index) => {
          if (this.firstWeekday >= index) {
            ele.innerHTML = this.dayArrBefore[this.dayArrBefore.length - (this.firstWeekday - index - 1)]
          }
        })

        // 渲染下个月残留日期
        let num = 0
        dayLine5.forEach((ele, index) => {
          if (this.lastWeekday <= index) {
            ele.innerHTML = this.dayArrAfter[index - num - 1]
          } else {
            num++
          }
        })

        // 渲染当前月份的所有日期

        dayLine1.forEach((ele, index) => {
          if (this.firstWeekday - 1 <= index) {
            dayIndex = index - (this.firstWeekday - 1)
            ele.innerHTML = this.dayArrNow[dayIndex]
          }
        })

        // 当月份开始时间5行放不下时
        dayLine0.forEach((ele, index) => {
          if (index - 6 >= this.firstWeekday) {
            ele.innerHTML = this.dayArrNow[index - 6 - this.firstWeekday]
          } else {
            ele.innerHTML = this.dayArrBefore[this.dayArrBefore.length - 13 + index + dayIndex]
          }
        })

        dayIndex = this.getMidDay(dayLine2, dayIndex)
        dayIndex = this.getMidDay(dayLine3, dayIndex)
        dayIndex = this.getMidDay(dayLine4, dayIndex)

        dayLine5.forEach((ele, index) => {
          if (this.dayArrNow[dayIndex + index + 1]) {
            ele.innerHTML = this.dayArrNow[dayIndex + index + 1]
          }
        })
      },
      /**
       *  渲染中间3行
       * @param {Arr} arr 用于遍历
       * @param {index} index 遍历开始的索引
       * */ 
      getMidDay (arr, dayIndex) {
        arr.forEach((ele, index) => {
          ele.innerHTML = this.dayArrNow[dayIndex + index + 1]
        })

        return dayIndex + 7
      },
      /**
       * 点击更换日期
       * @param {number} index 传入当前索引
       * @param {String} flag 判断是否为第一排额外多出天数
       */
      returnDay (index, flag) {
        if (index < this.firstWeekday || index - 29 > this.lastWeekday) {
          return
        } else if (this.firstWeekday <= 0 && flag) {
            this.day = this.dayArrNow[index - 7 - this.firstWeekday]
        } else {
          if (flag) {
            return
          } else {
            this.day = this.dayArrNow[index - this.firstWeekday]
            this.$emit('on-change', `${this.day}/${this.month}/${this.year}`)
          }
        }
      },
      /**
       * 点击更改月份
       * @param {String} 传入进入上个月或者下个月
       */
      changeMonth (flag) {
        if (flag === 'go') {
          this.month++
          if (this.month > 12) {
            this.year++
            this.month = 1
          }
          this.changeMonthItem()
        } else {
          this.month--
          if (this.month < 1) {
            this.year--
            this.month = 12
          }
          this.changeMonthItem()
        }
      },
      /**
       * 更改月份时的操作
       */
      changeMonthItem () {
        this.getDateNow()
        this.getFL()
        this.day = 1
        this.showDay()
      },
      /**
       * 生成每月第一天以及最后一天
       */
      getFL () {
        let lastWeekday = new Date(this.year, this.month, 0)

        this.lastWeekday = lastWeekday.getDay()
        this.firstWeekday = this.lastWeekday + 30 - this.dayArrNow.length
      }
    },
    mounted () {
      let date = new Date();
      let month = date.getMonth() + 1<10? "0"+(date.getMonth() + 1):date.getMonth() + 1
      let strDate = date.getDate()<10? "0" + date.getDate():date.getDate()
  
      this.year =  date.getFullYear()
      this.month = month
      this.day = strDate
      this.nowWeekday = date.getDay()

      this.getDateNow()
      this.getFL()

      this.$emit('on-change', `${this.day}/${this.month}/${this.year}`)
    }
  }
</script>

<style lang="scss" scoped>
  .unicorn-calendar-main {
    background-color: #efefef;
    border-radius: 6px;
    width: 320px;

    .unicorn-calendar-sec {
      display: flex;
      align-items: center;
      justify-content: space-between;
      height: 48px;
      padding: 0 15px;
      background-color: #FFF;
      border-radius: 6px;
      box-shadow: 0 0 5px rgba(0, 0, 0, .2);
      font-size: 14px;

      & img {
        cursor: pointer;
      }
    }

    .unicorn-calendar-choose-sec {
      margin-top: 10px;
      padding: 0 15px;
      height: 286px;
      border-radius: 6px;
      background-color: #FFF;

      .unicorn-calendar-choose-month {
        display: flex;
        align-items: center;
        justify-content: space-between;
        height: 50px;

        & img {
          cursor: pointer;
        }
      }

      .unicorn-calendar-choose-day-sec {

        .unicorn-calendar-choose-dayName {
          display: flex;
          justify-content: space-between;
          align-items: center;
          font-size: 12px;
          color: #cac2d0;

          & span {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 29px;
          }
        }

        .unicorn-line {
          display: flex;
          justify-content: space-between;
          align-items: center;
          margin-top: 5px;

          .unicorn-line-item {
            height: 1px;
            border-radius: 6px;
            width: 6px;
            background-color: #e9e8ea;
          }
        }

        .unicorn-day-sec {
          .unicorn-dayLine {
            display: flex;
            justify-content: space-between;
            margin: 5px 0;

            & :last-child {
              color: #ff9740 !important;
            }

            .unicorn-day {
              display: flex;
              justify-content: center;
              align-items: center;
              height: 29px; 
              width: 29px;
              font-size: 12px;
              border-radius: 50%;
              cursor: pointer;

              &:hover {
                background-color: #ebdaf0;
                color: #b649f0 !important;
              }
            }

            .unicorn-day-notnow {
              opacity: .2;
              cursor: not-allowed;

              &:hover {
                background-color: rgba(0, 0, 0, 0);
                color: #000 !important;
              }
            }

            .unicorn-nowDate {
              background-color: #a376b5;
              color: #FFF !important;
            }
          }

        }
      }
    }
  }
</style>