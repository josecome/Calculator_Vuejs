<template>
    <header>
      <h1>{{ title }}</h1>
      <Button
        @btn-click="toggleBackground"
        :text="changeBackground ? 'Bckg Blue' : 'Bckg White'"
        :color="changeBackground ? 'white' : 'blue'"
    />
    </header>
  </template>
  
  <script>
  import Button from './Button.vue'
  
  export default {
    name: 'Header',
    props: {
      title: String
    },
    components: {
      Button,
    },
    data(){
      return{
        changeBackground: false,
      }      
    },
    methods: {
      toggleBackground() {
      this.changeBackground = !this.changeBackground,
      this.$emit('toggle-bckg')
    }
  },
    
  }
  </script>
  
  <style scoped>
  header {
   margin-top: 30px;
   text-align: left;
  }
  </style>