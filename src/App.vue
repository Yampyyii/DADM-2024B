<script setup>
import { ref } from 'vue';
//modelo
const header = ref ('App lista de compras');

//items
//items model
const items = ref([
  {id:'0', label:'10 bolillos', purchased: true, priority:true},
  {id:'1', label:'1 lata de frijoles', purchased: false},
  {id:'2', label:'1 Chela', purchased: false},
  {id:'3', label:'1 Nutella', purchased: false},
]);
//item-method
const saveItem = ()=> {
items.value.push({id: items.value.length+1, label: newItem.value});
//clear the input
newItem.value="";
};
//formulario
const newItem= ref("");
const newItemHighPriority = ref(false);
const editing= ref(true);
const activateEdition=(activate)=>{
  editing.value= activate;

}

</script>
//metodos
<template>
<div class="header">

  <h1>
  <i 
  class="material-icons shopping-cart-icon">
   local_mall</i>
   {{ header }}
</h1>
<button v-if="editing" class="btn" 
@click="activateEdition(false)">
Cancelar
</button>
<button v-else class="btn btn-primary"
 @click="activateEdition(true)" >
 Agregar Articulo
</button>
</div>

<!--Agregando entradas de usuario-->
<form
class="add-item form"
v-if="editing"
v-on:submit.prevent="saveItem">

<!--Entrada de Texto-->
<input 
type="text"
placeholder="Add Item"
v-model.trim="newItem">
<!--Radio buttons-->
<label><input type="checkbox" v-model="newItemHighPriority">Alta prioridad</label>
<!--boton-->
<button
:disabled="newItem.length===0"
class="btn btn-primary">
Salvar Articulo
</button>

</form>

  <!--Lista-->
<ul>
 <li
  v-for="{label, id, purchased, priority} in items" 
  :key="id"
  class="amazing"
  :class="{ strikeout: purchased, priority: priority}">
 {{priority ? "🍻": "🥵"}}{{ label }}
</li>
</ul>
<p v-if="items.length === 0">🥀NO HAY ELEMENTOS EN LA LISTA🥀</p>
  </template>
<style scoped>
.shopping-cart-icon{
font-size: 2rem;
}
</style>

