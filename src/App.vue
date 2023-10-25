<script setup>
import { ref } from 'vue';
const header = ref('App Lista de compras');
const items = ref([
  {id: 1, label: '10 Galletas', purchased: true, highPriority: false},
  {id: 2, label: '1 lata de Duraznos', purchased: false, highPriority: true},
  {id: 3, label: '2 latas de Piña', purchased: true, highPriority: true}
]);
//Funcion que alterna el estado de comprado de un item
const togglePurchased = (item) => {
//Invertirla propiedad "purchased"
 item.purchased = !item.purchased;
}

// Agregado de metodo para guardar nuevo articulo en la lista
const saveItem = () => {
  items.value .push({id: items.value.length + 1, label: newItem.value})
  // limpiando el contenido  de newItems
  newItem.value ="";
};
const newItem = ref('');
const newItemHighPriority = ref(false);
const editing = ref(true);
const doEdit = (edit) => {
//Altero la variable "editing"
editing.value =edit;
//Limpio el input de texto
newItem.value= "";
};
</script>

<template>
  
  <div class="header">
  <h1> <i class="material-icons shopping-cart-icon">local_mall</i> {{ header }}</h1>
  <button v-if="!editing" @click="doEdit (true)" class="btn btn-primary">Agregar Articulo</button>
  <button v-else @click="doEdit(false)" class="btn">Cancelar</button>
  </div>

  <!--Enlazar un atributo
  <a v-bind:href="newItem">
  <i class="material-icons shopping-cart-icon"><link rel="stylesheet" href=""></i>
  </a> --> 

  <form v-if="editing" v-on:submit.prevent="saveItem" class="add-item form">

    <!-- Input de Nuevo Articulo -->
    <input v-model.trim="newItem" type="text" placeholder="Ingresar nuevo articulo">
    
    <!-- Check Boxes -->
    <label>
      <input v-model="newItemHighPriority" 
      type="checkbox">
      Alta Prioridad
    </label>
    {{ newItemHighPriority ? "🔥" : "🧊" }}
    <!-- Boton de UI -->
    <button :disabled="newItem.length === 0" class="btn btn-primary">Salvar Articulo</button>
  </form>
  <ul>
    <li 
    v-for = "({ id, label, purchased, highPriority}, index) in items" 
    v-bind:key="id"
    :class="{ strikeout : purchased, priority: highPriority}"
    @click="togglePurchased(items[index])"
    >
      🔹 {{ label }}
    </li>
  </ul>
  <p v-if="items.length === 0"> 🥀 lista de compras vacia 🥀 </p>
</template>

<style scoped>
.shopping-cart-icon {
  font-size: 2rem; /* Adjust the font-size value as per your desired size */
}
</style>