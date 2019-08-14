<template>
  <div class="unicorn-loading-box">
    <img class="unicorn-mawaru" src="./img/rotate.svg" alt="">
    <span>Loading</span>
  </div>
</template>

<script>
  export default {
    
  }
</script>

<style lang="scss" scoped>
.unicorn-loading-box {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 84px;
  height: 24px;

  .unicorn-mawaru {
    animation: mawaru 1s linear infinite;
  }

  @keyframes mawaru {
    0% {
      transform: rotate(0deg)
    }

    50% {
      transform: rotate(180deg)
    }

    100% {
      transform: rotate(360deg)
    }
  }
}
</style>