<script setup>
  import { ref, computed } from 'vue';

  const editing = ref(false)
  const items = ref([ 
    // {id: 1, label: "10 tomates", purchased: true, highPriority: false},
    // {id: 2, label: "5 chocolates", purchased: true, highPriority: false},
    // {id: 3, label: "2 gaseosas", purchased: false, highPriority: true},
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
  <div class="header-container">
    <h1> Shopping List App with Vue</h1>
    <button v-if="editing" @click="doEdit(false)" class="btn-cancel">Cancelar</button>
    <button v-else @click="doEdit(true)" class="btn-add">Añadir Producto</button>
  </div>

  <div class="main-container">
    <form @submit.prevent="saveItems" v-if="editing">
      <input v-model.trim="newItem" type="text" placeholder="Añadir producto" class="text-input">
      <label class="checkbox">
        <input type="checkbox" v-model="newItemHightPriority">Muy importante
      </label>
      <button :disabled="newItem.length < 2">Añadir a la lista</button>
    </form>
    <ul>
      <li v-for="(item, index) in reversedItems" @click="togglePurchased(item)" :key="item.id" :class="{priority: item.highPriority, strikeout: item.purchased}">{{ item.label }}</li>
    </ul>
    <p v-if="!items.length">Lista vacia</p>
  </div>
</template>

<style lang="scss">
  @import './assets/styles.scss';
  
</style>
