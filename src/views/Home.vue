<template>
  <div class="home">
    <!-- <Page pages="101"></Page> -->
    <Box-line></Box-line>
  </div>
</template>

<script>
// @ is an alias to /src
import Page from '@/components/Page/Page.vue'
import BoxLine from '../components/BoxLine/boxLine'

export default {
  name: 'home',
  methods: {

  },
  components: {
    Page,
    BoxLine
  }
}
</script>
