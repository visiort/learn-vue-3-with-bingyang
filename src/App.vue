<template>
  <h1>{{ message }}</h1>

  <div class="card">
    <h1>Scenarion 1L Watch a "ref(primitive value)"</h1>
    <h2>Number: {{ number }}</h2>
    <button @click="number++">Increment number by 1</button>
  </div>
</template>

<script setup>
  import {ref} from 'vue'

  let message = ref('Hello, Watchers!!')

  let number = ref(1)

  let stopWatch = watch(
    number, 
    (newValue, oldValue) => {
      console.log(
        'Watch a ref(primitive value): number changes',
        newValue,
        oldValue
      )
      if (newValue > 5) {
        stopWatch()
      }
  },
  {immediate: true}
)

</script>

<style scoped>
  .card {
    background-color: purple;
    color: white;
    padding: 20px 10px;
    margin-bottom: 10px;
  }
</style>