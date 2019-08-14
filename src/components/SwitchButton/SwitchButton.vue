<template>
  <div @click="changeSwitch" 
  :class="{'unicorn-switch-sec-change': open && disabled === 'default',
  'unicorn-switch-sec-disabled': disabled === 'disabled'}"
  class="unicorn-switch-sec">
    <div class="unicorn-button" 
    :class="{'unicorn-button-sel': open}"></div>
  </div>
</template>

<script>
  export default {
    props: {
      // 是否禁用
      disabled: {
        type: String,
        default: 'default',
        validator (value) {
          return value === 'default'|| value === 'disabled'
        }
      }
    },
    data () {
      return {
        open: false
      }
    },
    methods: {
      changeSwitch () {
        if (this.disabled === 'default') {
          this.open = !this.open
  
          this.$emit('on-change', this.open)
        } else {
          return
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
.unicorn-switch-sec {
  display: flex;
  align-items: center;
  padding: 0 2px;
  border-radius: 16px;
  width: 46px;
  height: 28px;
  background-color: #ECE9F1;
  cursor: pointer;
  transition: all .3s ease-in-out;

  .unicorn-button {
    height: 24px;
    width: 24px;
    background-color: #D0C9D6;
    border-radius: 50%;
    transition: all .3s ease-in-out;
  }

  .unicorn-button-sel {
    background-color: #9863d1;
    transform: translateX(22px);
    transition: all  .3s ease-in-out;
  }
}

.unicorn-switch-sec-change {
  background-color: #e7d8f6;
}

.unicorn-switch-sec-disabled {
  cursor: not-allowed;
}
</style>