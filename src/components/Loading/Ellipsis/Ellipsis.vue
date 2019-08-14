<template>
  <div class="unicorn-dot-sec">
    <span class="unicorn-dot unicorn-fir-dot"></span>
    <span class="unicorn-dot unicorn-sec-dot"></span>
    <span class="unicorn-dot unicorn-thi-dot"></span>
  </div>
</template>

<script>
  export default {
    
  }
</script>

<style lang="scss" scoped>
.unicorn-dot-sec {
  display: flex;
  justify-content: space-between;
  width: 20px;
  height: 15px;

  .unicorn-dot {
    position: relative;
    display: block;
    height: 5px;
    width: 5px;
    background-color: #5e6ef7;
    border-radius: 50%;
  }

  .unicorn-fir-dot {
    animation: firDot 1s linear infinite;
  }

  .unicorn-sec-dot {
    animation: serDot 1s linear infinite;
    animation-delay: calc(1 * 0.25s);
  }

  .unicorn-thi-dot {
    animation: thiDot 1s linear infinite;
    animation-delay: calc(1 * 0.5s);
  }

  // 第一个点的运动
  @keyframes firDot {
    0% {
      transform: translateY(0px);
    }
    
    50% {
      transform: translateY(-5px);
    }

    100% {
      transform: translateY(0px);
    }
  }

  // 第二个点的运动
  @keyframes serDot {
    0% {
      transform: translateY(0px);
    }
    
    50% {
      transform: translateY(-5px);
    }

    100% {
      transform: translateY(0px);
    }
  }

  // 第三个点的运动
  @keyframes thiDot {
    0% {
      transform: translateY(0px);
    }
    
    50% {
      transform: translateY(-5px);
    }

    100% {
      transform: translateY(0px);
    }
  }
}
</style>