<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Home from './views/Home.vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div id="main">
    <Header />
    <router-view></router-view>
    <Footer v-show="homePage" />
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
  computed: {
    homePage() {
        if (this.$route.path === '/') {
          return true
        } else {
          return false
        }
      },
  }
}
</script>
<style scoped>
#main{
  margin-top: 30px;
  text-align: center;
  margin: auto;
  width: 50%;
}
</style>
