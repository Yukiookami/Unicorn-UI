<template>
  <div class="unicorn-number-box" 
  :class="{'unicorn-number-fir-box': index === 1,
  'unicorn-number-sle-box': index <= current && index !== 1, 
  'unicorn-number-doing-box': index === current && index !== 1, 
  'unicorn-number-sle-box-show': index === current - 1,
  'unicorn-number-fal-box-show': current === total}">
    <img v-if="index < current" src="./img/ok.svg" alt="">
    <span v-else>{{index}}</span>
  </div>
</template>

<script>
  export default {
    name: 'Step',
    props: {
      // 当前步骤数
      index: {
        type: Number
      },
      // 当前进行到步骤数
      current: {
        type: Number
      },
      // 总步骤数
      total: {
        type: Number
      }
    }
  }
</script>

<style lang="scss" scoped>
.unicorn-number-box {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 29px;
  width: 29px;
  border: 1px #ECEBED solid;
  color: #ECEBED;
  border-radius: 50%;
  font-size: 14px;
  margin: 0 80px;
  transition: all .3s ease-in-out;

  &::before,
  &::after {
    content: '';
    position: absolute;
    display: block;
    height: 2px;
    width: 85px;
    background-color: #ECEBED;
  }

  &::before {
    left: 33px;
  }

  &::after {
    right: 33px;
  }
}

.unicorn-number-fir-box {
  background-color: #6979F8;
  border: 1px #6979F8 solid;
  color: #FFF;

  &::after {
    content: '';
    position: absolute;
    display: block;
    height: 2px;
    width: 85px;
    background-color: #6979F8;
  }

  &::after {
    right: 33px;
  }
}

.unicorn-number-sle-box {
  background-color: #6979F8;
  border:1px #6979F8 solid;
  color: #FFF;

  &::after {
    content: '';
    position: absolute;
    display: block;
    height: 2px;
    width: 154px;
    background-color: #6979F8;
  }

  &::after {
    left: -158px;
  }
}

.unicorn-number-doing-box {
  animation: duang .3s ease-in-out;
  background-color: #6979F8;
  border: 1px #6979F8 solid;
  color: #FFF;

  @keyframes duang {
    0% {
      background-color: #ECEBED;
      border: 1px #ECEBED solid;
      color: #ECEBED;
    }

    100% {
      background-color: #6979F8;
      border: 1px #6979F8 solid;
      color: #FFF;
    }
  }

  &::after {
    content: '';
    position: absolute;
    display: block;
    height: 2px;
    width: 154px;
    background-color: #6979F8;
    animation: biu .3s ease-in-out alternate;
  }

  &::after {
    left: -158px;
  }

  @keyframes biu {
    0% {
      width: 0px
    }

    100% {
      width: 154px
    }
  }
}

.unicorn-number-sle-box-show {
  &::before {
    width: 154px;
  }
}

.unicorn-number-fal-box-show {
  &::before {
    animation: biubiu ease-in-out .3s;
    background-color: #6979F8;
  }

  @keyframes biubiu {
    0% {
      background-color: #ECEBED;
    }

    100% {
      background-color: #6979F8;
    }
  }
}
</style>