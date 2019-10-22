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
body {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
