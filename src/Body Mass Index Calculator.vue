<script setup>
import { ref } from "vue";
import BodyMassIndexForm from './components/BodyMassIndexForm.vue';

const useMetric = ref(true); // Will allow users to switch between imperial and metric units

// Store BMI value
const bmi = ref(null);

//Calculate BMI based on measurement choice
const calculateBMI = ({ height, weight }) => {
  if (useMetric.value) {
    bmi.value = weight / (height * height);
  } else {
    bmi.value = (weight / (height * height)) * 730;
  }
};

//Clears data when new measurement is selected
const clearData = () => {
  bmi.value = null;
};

</script>


<template>
  <div class="app">
    <h1>Body Mass Index Calculator</h1>
    <label>
      
      <!--Checkbox for user to switch between imperial and metric units-->
      <input type="checkbox" v-model="useMetric" @change="clearData" />
      Use metric units
    </label>
    <BodyMassIndexForm @stats-entered="calculateBMI" :useMetric="useMetric" />
    <p v-if="bmi !== null">Your BMI: {{ bmi.toFixed(2) }}</p>
  </div>
</template>

<style scoped>

</style>
