<template>
  <div class="home">
    <HelloWorld msg="Welcome to Your Vue.js + Flask App"/>
    <chart/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import chart from '@/components/chart.vue'
export default {
  name: 'home',
  components: {
    HelloWorld, chart
  }
}
</script>

<style lang="scss">

</style>
