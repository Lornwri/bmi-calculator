<script setup>
import HelloWorld from './components/bmi-calculator.vue'
</script>

<template>
  <div class="app">
    <h1>Body Mass Index Calculator</h1>
    <label>
      <input type="checkbox" v-model="useMetric" @change="clearData" />
      Use metric units
    </label>
    <BodyMassIndexForm @stats-entered="calculateBMI" :useMetric="useMetric" />
    <p v-if="bmi !== null">Your BMI: {{ bmi.toFixed(2) }}</p>
  </div>
</template>

<style scoped>

</style>
