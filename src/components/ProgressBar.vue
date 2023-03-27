<template>
    <div>
      <h2> barre de progression</h2>
      <progress :value="progressValue" max="100"></progress>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    setup() {
      const progressValue = ref(0);
  
      // Exemple d'incrémentation de la barre de progression toutes les secondes
      setInterval(() => {
        if (progressValue.value < 100) {
          progressValue.value += 10;
        } else {
          progressValue.value = 0;
        }
      }, 1000);
  
      return {
        progressValue,
      };
    },
  };
  </script>