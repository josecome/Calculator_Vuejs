<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Home from './views/Home.vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'

</script>

<template>
  <div id="main" :class="changeBackground ? 'bck' : 'bck2'">
    <Header 
      title="Calculator"
      @toggle-bckg = "toggleBackground"      
    />
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
      changeBackground: false
    }
  },
  methods: {
    toggleBackground() {
      console.log('Changed!'),
      this.changeBackground = !this.changeBackground
    }
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
  display: table;
}
.bck{
  background-color: #85C1E9;
}
.bck2{
  background-color: white;
}
</style>
