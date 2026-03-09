<template>
  <h1>{{ message }}</h1>

  //Scenario 1
  <div class="card">
    <h1>Scenarion 1: Watch a "ref(primitive value)"</h1>
    <h2>Number: {{ number }}</h2>
    <button @click="number++">Increment number by 1</button>
  </div>

  //Scenario 2
  <div class="card">
    <h1>Scenarion 2: Watch a property in a "ref(object)"</h1>
    <h2>Number: {{ wizard1.name }}</h2>
    <h2>Wand: {{ wizard1.wand }}</h2>
    <button @click="wizard1.name = wizard1.name.toUpperCase()">
      Change name to upper case
    </button>
    <button @click="changeWizardWand">Change wand</button>
    <button @click="wizard1.wand.core = 'Unicord hair'">
      Change wand core
    </button>
  </div>

  //Scenario 3
  <div class="card">
    <h1>Scenarion 3: Watch a "ref(object)"</h1>
    <h2>Number: {{ wizard2.name }}</h2>
    <h2>Wand: {{ wizard2.wand }}</h2>
    <button @click="wizard2.name = wizard2.name.toUpperCase()">
      Change name to upper case
    </button>
    <button @click="wizard2.wand.core = 'Phoenix feather'">
      Change wand core
    </button>
    <button @click="changeWizard">Change wizard</button>
  </div>

  //Scenario 4
</template>

<script setup>
  import {ref} from 'vue'

  let message = ref('Hello, Watchers!!')

  //Scenario 1
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
  {immediate: true})


  //Scenario 2
  let wizard1 = ref({
    id: 1001,
    name: 'Harry Potter',
    house: 'Gryffindor',
    age: 17, 
    wand: {
      core: 'Phoenix feather',
      wood: 'Holly'
    }
  })

  function changeWizardWand() {
    wizard1.value.wand = {
      core: 'Dragon heartstring',
      wood: 'Vine'
    }
  }

  watch(()=> wizard1.value.name,(newValue, oldValue) => {
    console.log('Watch a property in a ref(object): wizard1 name changes', newValue, oldValue)
  })

  watch(()=>wizard1.value.wand, (newValue, oldValue)=> {
    console.log('Watch a property in a ref(object): wizard1 wand changes', newValue, oldValue)
  },
  {deep: true})

  //Scenario 3
  function changeWizard() {
    wizard2.value = {
      id: 1002,
      name: 'Hermione Granger',
      house: 'Gryffindor',
      age: 17, 
      wand: {
        core: 'Dragon heartstring',
        wood: 'Vine'
      }
  }}

  watch(wizard2, (newValue, oldValue)=>{
    console.log('Watch a ref(object): wizard2 cahnges', newValue, oldValue)
  },
  {deep: true})

  //Scenario 4
  watch([number, ()=> wizard1.value.name, wizard2],
  (newValue, oldValue)=> {
    console.log('Watch an array of ref(primitive value), a property of a ref(object) and a ref(object)')
  },
  {deep: true})

</script>

<style scoped>
  .card {
    background-color: purple;
    color: white;
    padding: 20px 10px;
    margin-bottom: 10px;
  }
</style>