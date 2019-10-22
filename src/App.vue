<template>
  <div id="app">
    <main>
      <Chart />
    </main>
  </div>
</template>

<script>
import Chart from './components/Chart.vue'

export default {
  name: 'app',
  components: {
    Chart
  }
}
</script>

<style>
html {
  background: #161616;
  text-align: center;
}
</style>
