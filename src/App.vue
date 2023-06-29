<script setup>
  import { ref } from 'vue';

  const header = ref ('Shopping List App')
  const items = ref([ 
    {id: 1, label: "10 tomates"},
    {id: 2, label: "5 chocolates"},
    {id: 3, label: "2 gaseosas"},
  ])

  const newItem = ref("")
  const newItemHightPriority = ref("low")
</script>

<template>
  <h1> {{ header }}</h1>

  <form @submit.prevent="items.push({id: items.length + 1, label: newItem})">
    <input v-model.trim="newItem" type="text" placeholder="Añadir producto"> {{ newItem }}
    <label>
      <input type="checkbox" v-model="newItemHightPriority">Muy importante
    </label>
    <button>Añadir a la lista</button>
  </form>
  <ul>
    <li v-for="({id, label}, index) in items" :key="id">{{ label }}</li>
  </ul>
</template>

<style lang="scss">
  @import './assets/styles.scss';
</style>
