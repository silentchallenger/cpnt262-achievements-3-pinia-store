<script setup lang="ts">
import { storeToRefs } from 'pinia';
import { useCounterStore } from './stores/useCounter';

const main = useCounterStore();

const { counter, name, doubleCount } = storeToRefs(main);

function add(value: number) {
  main.$patch ({
    counter: counter.value + value
  });
}

function remove(value: number) {
  main.$patch ({
    counter: counter.value - value
  });
}

function reset() {
  main.$reset();
}

main.$subscribe((mutation, state) => {
  console.log("mutation", mutation);
  console.log("state", state);
})

</script>

<template>
  <h3>Hello {{ name }}</h3>
  <h4>Count: {{ counter }}</h4>
  <button @click="main.addOne">Add +1</button>
  <button @click="add(10)">Add +10</button>
  <button @click="main.removeOne">Remove -1</button>
  <button @click="remove(10)">Remove -10</button>
  <button @click="reset">Reset</button>
</template>

<style scoped>
#app {
  text-align: center;
  margin-top: 50px;
}

</style>
