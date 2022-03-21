<script setup lang="ts">
import { computed, ref } from 'vue'

let test = ref<string>('');

const error = computed(() => {
  return {
    text: typeof rules.value(test.value) === "string" ? rules.value(test.value) : "",
    color: typeof rules.value(test.value) === "string" ? "red" : "rgb(94, 93, 93)"
  }
});


const rules = computed(() => {
  return (x: string) => !!x || "O campo é obrigatório"
});
</script>

<template>
  <input id="input" placeholder="testando" v-model="test" />
  <span v-if="error.text" style="color: red">{{ error.text }}</span>
</template>

<style scoped>
input {
  padding: 0.5%;
  border: 1px solid rgb(145, 145, 145);
  border-radius: 0.5em;
  color: rgb(94, 93, 93);
}
input:focus {
  outline: 1px solid v-bind("error.color");
}
</style>