<template>
  <div class="unicorn-mappin-sec unicorn-mappin-sec-ajirushi"
  :class="{'unicorn-mappin-sec-default': size === 'default',
  'unicorn-mappin-sec-large': size === 'large',
  'unicorn-ajirushi-bottom-large': size === 'large' && direction === 'bottom',
  'unicorn-ajirushi-right-large': size === 'large' && direction === 'right',
  'unicorn-ajirushi-left-large': size === 'large' && direction === 'left',
  'unicorn-mappin-sec-small': size === 'small',
  'unicorn-ajirushi-bottom-small': size === 'small' && direction === 'bottom',
  'unicorn-ajirushi-right-small': size === 'small' && direction === 'right',
  'unicorn-ajirushi-left-small': size === 'small' && direction === 'left',
  'unicorn-ajirushi-bottom': direction === 'bottom',
  'unicorn-ajirushi-right': direction === 'right',
  'unicorn-ajirushi-left': direction === 'left'}">
    <div class="content-box" v-html="content"></div>
  </div>
</template>

<script>
  export default {
    props: {
      // 聊天框里的内容
      content: {
        type: String
      },
      // 尺寸
      size: {
        type: String,
        default: 'default',
        validator (value) {
          const relValue = ['default', 'large', 'small']
          return relValue.indexOf(value) !== -1
        }
      },
      // 朝向
      direction: {
        type: String,
        default: 'bottom',
        validator (value) {
          const relValue = ['left', 'right', 'bottom']
          return relValue.indexOf(value) !== -1
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
.unicorn-mappin-sec {
  padding: 10px;
  position: relative;
  background-color: #6979F8;
  border-radius: 18px;

  & .content-box {
    word-wrap: break-word;
    word-break: normal;
    color: #FFF;
  }
}

.unicorn-mappin-sec-default {
  min-height: 86px;
  max-width: 86px;
}

.unicorn-mappin-sec-large {
  min-height: 148px;
  max-width: 148px;
}

.unicorn-mappin-sec-small {
  min-height: 40px;
  max-width: 40px;
}

.unicorn-mappin-sec-ajirushi {
  &::after {
    content: '';
    display: block;
    height: 0;
    width: 0;
    border-width: 0px 10px 8px 10px;
    border-style: solid;
    border-color: transparent transparent #6979F8;
  }
}

.unicorn-ajirushi-bottom {
  &::after {
    position: absolute;
    top: 100%;
    left: 39%;
    transform: rotate(180deg);
  }
}

.unicorn-ajirushi-right {
  &::after {
    position: absolute;
    right: 94%;
    top: 48%;
    transform: rotate(-90deg);
  }
}

.unicorn-ajirushi-left {
  &::after {
    position: absolute;
    left: 94%;
    top: 48%;
    transform: rotate(90deg);
  }
}

.unicorn-ajirushi-bottom-large {
  &::after {
    left: 43%;
    border-width: 0px 14px 10px 14px;
  }
}

.unicorn-ajirushi-left-large {
  &::after {
    border-width: 0px 14px 10px 14px;
  }
}

.unicorn-ajirushi-right-large {
  &::after {
    border-width: 0px 14px 10px 14px;
  }
}

.unicorn-ajirushi-bottom-small {
  &::after {
    left: 38%;
    border-width: 0px 6px 5px 6px;
  }
}

.unicorn-ajirushi-right-small {
  &::after {
    border-width: 0px 6px 5px 6px;
  }
}

.unicorn-ajirushi-left-small {
  &::after {
    border-width: 0px 6px 5px 6px;
  }
}
</style>