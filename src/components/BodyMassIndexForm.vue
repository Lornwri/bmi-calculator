<script setup>
import { ref, watch } from 'vue'

const props = defineProps(['useMetric']);
const emit = defineEmits(['stats-entered']);

//Reactive variables for input and input errors
const height = ref('');
const weight = ref('');
const heightError = ref('');
const weightError = ref('');

//Validate user input
const validateInput = () => {
  const maxHeight = props.useMetric ? 3 : 108; // Maximum height in meters or inches
  const maxWeight = props.useMetric ? 500 : 1100; // Maximum weight in kg or lbs

  //If no data is entered - or incorrect - error message will show
  heightError.value =
      height.value <= 0 || height.value > maxHeight ? 'Invalid height' : '';
  weightError.value =
      weight.value <= 0 || weight.value > maxWeight ? 'Invalid weight' : '';
};

//Emit to parent with valid values for height and weight
const handleCalculate = () => {
  if (!heightError.value && !weightError.value) {
    emit('stats-entered', { height: parseFloat(height.value), weight: parseFloat(weight.value) });
  }
};

// Clear when the unit changes
watch(
    () => props.useMetric,
    () => {
      height.value = '';
      weight.value = '';
      heightError.value = '';
      weightError.value = '';
    }
);
</script>

<template>
  <div class="form">
    <label>
      Height ({{ useMetric ? 'meters' : 'inches' }}):
      <input type="number" v-model="height" @input="validateInput" />
    </label>
    <span v-if="heightError" class="error">{{ heightError }}</span>

    <label>
      Weight ({{ useMetric ? 'kilograms' : 'pounds' }}):
      <input type="number" v-model="weight" @input="validateInput" />
    </label>
    <span v-if="weightError" class="error">{{ weightError }}</span>

    <button @click="handleCalculate">Calculate</button>
  </div>

</template>

<style scoped>

</style>
