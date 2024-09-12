<script setup>
import {ref} from "vue";

const fruits = ref([
  {id: 1, name: "Apfel", value: "apple"},
  {id: 2, name: "Banane", value: 'banana'},
  {id: 3, name: "Himbeere", value: 'raspberry'},
  {id: 4, name: "Ananas", value: 'pineapple'},
  {id: 5, name: "Aprikose", value: 'apricot'},
]);

</script>

<template>
  <div class="container" v-for="fruit in fruits">
    {{ fruit.name }}
  </div>

</template>

<style scoped>
/* Styling for the select element */
select {
  width: 200px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  background-color: #fff;
  font-size: 16px;
  color: #333;
  outline: none;
  appearance: none;
  cursor: pointer;
}

/* Adding some custom arrow styling */
select::-ms-expand {
  display: none; /* For IE */
}

/* Option element styling */
select option {
  padding: 10px;
}


</style>