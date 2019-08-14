<template>
  <div @click="change" class="unicorn-dot unicorn-dot-default" 
  :class="{'unicorn-dot-white-sel': index === selNum && color === 'white',
  'unicorn-dot-default-sel': index === selNum && color === 'default'}"></div>
</template>

<script>
  export default {
    props: ['color', 'selNum', 'index'],
    methods: {
      change () {
        this.$emit('changeDot', this.index)
      }
    }
  }
</script>

<style lang="scss" scoped>
.unicorn-dot {
  border-radius: 50%;
  height: 8px;
  width: 8px;
  cursor: pointer;
  transition: all .3s ease-in-out;
}

.unicorn-dot-default {
  background-color: #e9e6ef;
}

.unicorn-dot-default-sel {
  background-color: #5e6ef7;
}

.unicorn-dot-white-sel {
  background-color: #FFF;
}
</style>