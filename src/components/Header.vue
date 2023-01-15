<template>
    <header>
      <h1>{{ title }}</h1>

    </header>
  </template>
  
  <script>
  import Button from './Button.vue'
  
  export default {
    name: 'Header',
    props: {
      title: String,
      CalculatorType: Boolean,
    },
    components: {
      Button,
    }
  }
  </script>
  
  <style scoped>
  header {
   margin-top: 30px;
   text-align: left;
  }
  </style>