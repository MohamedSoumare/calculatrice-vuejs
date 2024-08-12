<template>
  <div>
    <h1> Calculatrice</h1>
    
    <div class="form-group">
      <label for="operation">Choisir une operation:</label>

      <div id="operation" class="form-check">
        <input v-model="operation" type="radio" id="add" value="add" class="form-check-input">
        <label for="add" class="form-check-label">Addition</label>
      </div>
      
      <div class="form-check">
        <input v-model="operation" type="radio" id="subtract" value="subtract" class="form-check-input">
        <label for="subtract" class="form-check-label">Soustraction</label>
      </div>

      <div class="form-check">
        <input v-model="operation" type="radio" id="multiply" value="multiply" class="form-check-input">
        <label for="multiply" class="form-check-label">Multiplication</label>
      </div>
      
      <div class="form-check">
        <input v-model="operation" type="radio" id="divide" value="divide" class="form-check-input">
        <label for="divide" class="form-check-label">Division</label>
      </div>

    </div>

    <div v-if="operation" class="mt-4">
      <div class="form-group">
        <label for="value1">Entre votre permiére  valeur:</label>
        <input v-model="value1" type="number" id="value1" class="form-control" placeholder="First value">
      </div>

      <div class="form-group mt-2">
        <label for="value2">Entre votre seconde valeur:</label>
        <input v-model="value2" type="number" id="value2" class="form-control" placeholder="Second value">
      </div>

      <button @click="calculate" class="btn btn-success mt-4">Calculer</button>
    </div>

    <Result :result="result" :error="error" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Result from './Result.vue';

const operation = ref(null);
const value1 = ref(null);
const value2 = ref(null);
const result = ref(null);
const error = ref('');

const calculate = () => {
  error.value = '';
  result.value = null;

  if (value1.value === null || value2.value === null) {
    error.value = 'Veuillez saisir les deux valeurs.';
    return;
  }

  switch (operation.value) {
    case 'add':
      result.value = parseFloat(value1.value) + parseFloat(value2.value);
      break;
    case 'subtract':
      result.value = parseFloat(value1.value) - parseFloat(value2.value);
      break;
    case 'multiply':
      result.value = parseFloat(value1.value) * parseFloat(value2.value);
      break;
    case 'divide':
      if (parseFloat(value2.value) === 0) {
        error.value = 'Impossible de faire division par zéro.';
      } else {
        result.value = parseFloat(value1.value) / parseFloat(value2.value);
      }
      break;
    default:
      error.value = 'L\'operation n\'est valide.';
  }
};
</script>

<style scoped>

</style>

