<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Home from './views/Home.vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div>
    <Header />
    <router-view></router-view>
    <Footer />
  </div>
    
</template>

<script>
export default {
  name: 'App',
  components: {
    Header,
    Footer,
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
