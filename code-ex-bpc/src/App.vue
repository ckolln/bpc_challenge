<template>
  <div id="app">
    <div class="skin1">
      <skin1/>
    </div>
    <div class="skin2">
    <skin2/>
    </div>
  </div>
</template>

<script>
import skin1 from './components/skin1.vue'
import skin2 from './components/skin2.vue'

export default {
  name: 'app',
  components: {
    skin1,
    skin2
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  display:inline-flex;
}

.skin1 {
  margin: 100px;
  display: inline-flex;
  overflow: visible;
}

.skin2 {
  margin-top: 120px;
  display: inline-flex;
}

html {
  background-color: #d9e8e6;
}
</style>
