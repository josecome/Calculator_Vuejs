<template>
  <main>
    <Button
        @btn-click="ChangeCalculator"
        :text="!calc ? 'Scientific' : 'Standard'"
        :color="'white'"
        style="float: right"
    /><br />
    <Calculator
     v-if="calculator_type === 'Standard'" />
     <S_Calculator
     v-if="calculator_type === 'Scientific'" />     
  </main>
</template>

<script>
 import Calculator from '../components/Calculator.vue'
 import S_Calculator from '../components/Scientific_Calculator.vue'
 import Button from '../components/Button.vue'
export default {
  name: 'Home',
  components: {
    Calculator,
    S_Calculator,
    Button
  },
  data() {
    return {
      calculator_type: 'Standard',
      calc: false
    }
  },
  methods: {
    ChangeCalculator() {
      this.calc = !this.calc;
      this.calc ? this.calculator_type = 'Scientific' : this.calculator_type = 'Standard';   
      
    }
  }
}
</script>