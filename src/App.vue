<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Home from './views/Home.vue'
</script>

<template>
  <div>
    <Home />
  </div>
    
</template>

<script>
export default {
  name: 'App',
  components: {
    Home
  },
  data() {
    return {
      
    }
  },
  methods: {
    
  },
}
</script>
<style scoped>


</style>
