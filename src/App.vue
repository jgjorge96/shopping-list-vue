<script setup>
  import { ref, computed } from 'vue';

  const header = ref ('Shopping List App')
  const editing = ref(false)
  const items = ref([ 
    {id: 1, label: "10 tomates", purchased: true, highPriority: false},
    {id: 2, label: "5 chocolates", purchased: true, highPriority: false},
    {id: 3, label: "2 gaseosas", purchased: false, highPriority: true},
  ])
  const reversedItems = computed(()=> [...items.value].reverse() )

  const newItem = ref("")
  const newItemHightPriority = ref("low")
  const saveItems = () => {
    items.value.push({id: items.value.length + 1, label: newItem.value, highPriority: newItemHightPriority.value})
    newItem.value = ""
    newItemHightPriority.value= ""
  }
  const doEdit = (e) => {
    editing.value = e
    newItem.value = ""
    newItemHightPriority.value= ""
  }
  const togglePurchased = (item) => {
    item.purchased= !item.purchased
  }
</script>

<template>
  <div>
    <h1> {{ header }}</h1>
    <button v-if="editing" @click="doEdit(false)">Cancelar</button>
    <button v-else @click="doEdit(true)">Añadir Producto</button>
  </div>

  <form @submit.prevent="saveItems" v-if="editing">
    <input v-model.trim="newItem" type="text" placeholder="Añadir producto">
    <label>
      <input type="checkbox" v-model="newItemHightPriority">Muy importante
    </label>
    <button :disabled="newItem.length < 2">Añadir a la lista</button>
  </form>
  <ul>
    <li v-for="(item, index) in reversedItems" @click="togglePurchased(item)" :key="item.id" :class="{strikeout: item.purchased, priority: item.highPriority}">{{ item.label }}</li>
  </ul>
  <p v-if="!items.length">Lista vacia</p>
</template>

<style lang="scss">
  @import './assets/styles.scss';
  .strikeout {
    color: blue;
  }
  .priority {
    color: red;
  }
</style>
