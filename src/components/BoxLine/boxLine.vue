<template>
  <div class="main-sec">
    <div class="first-box">

    </div>

    <div class="link-sec">
      <div class="content-box">

      </div>

      <div class="content-box">

      </div>
    </div>
  </div>
</template>

<script>
  export default {
    
  }
</script>

<style lang="scss" scoped>
  .main-sec {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 100%;

    .first-box {
      position: relative;
      height: 32px;
      width: 64px;
      border: 1px #333 solid;

      &::after {
        content: '';
        position: absolute;
        bottom: -25px;
        left: 32px;
        height: 24px;
        border-left: #333 solid .5px;
      } 
    }

    .content-box {
      position: relative;
      height: 32px;
      width: 64px;
      border: 1px #333 solid;

      &::after {
        content: '';
        position: absolute;
        top: -24px;
        left: 32px;
        height: 24px;
        border-left: #333 solid .5px;
      } 
    }

    .link-sec {
      position: relative;
      display: flex;
      width: 160px;
      justify-content: space-between;
      margin: 32px 0;
      padding-top: 16px; 

      &::after {
        content: '';
        position: absolute;
        left: 33px;
        top: -8px;
        border-top: .5px solid #333;
        width: 95px;
      }
    }
  }
</style>