<template>
  <div :class="['app']">
    <main class="container">
      <KomponenInduk/>
    </main>
  </div>
</template>

<script>
import KomponenInduk from './components/KomponenInduk.vue'

export default {
  name: 'App',
  components: {
    KomponenInduk
  },
  data() {
    return {
      isDarkMode: false
    }
  }
}
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-color: #f5f7fa;
  min-height: 100vh;
}


.container {
  max-width: 768px;
  width: 100%;
  margin: 0 auto;
  padding: 20px;
}
</style>
