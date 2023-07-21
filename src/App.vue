<script setup>
import {ref, computed} from "vue";
  const contador = ref(0);
  const arrayNumeros = ref([]);
  const incrementar = ()=>{
    contador.value++;
  }
  const decrementar = ()=>{
    contador.value--;
  }
  const resetear = ()=>{
    contador.value = 0;
  }
  const agregar = ()=>{
    arrayNumeros.value.push(contador.value);
  }
  const eliminar = (indice)=>{
    arrayNumeros.value.splice(indice, 1);
    //console.log(arrayNumeros.value);
    //falta mostrar los datos invertidos
    //pero hay un problema con el indice pi pi pi
  }
  //Usar computed siempre que necesites crear propiedades 
  //que dependan de otras propiedades reactivas o 
  //cuando necesites optimizar el rendimiento de tus cálculos.
  const bloquearNumero = computed(()=>{
    const numero = arrayNumeros.value.find((num)=> num === contador.value);
    return numero || numero === 0;
  });

  const classContador = ()=>{
    if(contador.value > 0){
      return "display-1 text-primary-emphasis text-center";
    } else if (contador.value < 0) {
      return "display-1 text-danger-emphasis text-center";
    } else {
      return "display-1 text-center";
    }
  };
</script>

<template>
  <div class="container d-flex justify-content-center align-items-center" style="min-height: 100vh;">
    <div class="row">
      <div class="col align-self-center">
        <ul class="list-group">
          <li v-for="(item, index) in arrayNumeros" 
          :key="index" @click="eliminar(index)"
          class="list-group-item list-group-item-warning text-center">
            {{ item }}
          </li>
        </ul>
      </div>
      <div class="col align-self-center col-xs-12">
        <h1 :class="classContador()">
          {{ contador }}
        </h1>
        <div class="btn-group-vertical" role="group">
          <button type="button" class="btn btn-outline-primary" @click="incrementar">Incrementar</button>
          <button type="button" class="btn btn-outline-primary" @click="decrementar">Decrementar</button>
          <button type="button" class="btn btn-outline-primary" @click="resetear">Resetear</button>
          <button type="button" class="btn btn-primary" @click="agregar" :disabled="bloquearNumero">Agregar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
li:hover {
  cursor: pointer;
  color: #750101; /* Cambia "red" al color que desees cuando se pase el mouse por encima */
  text-decoration: line-through; /* Añade una línea de tachado al texto del elemento */
}
</style>