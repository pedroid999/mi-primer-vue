<script setup>
import  {ref, computed} from 'vue'

const name = "Vue 3"
let numberClass = 'numberZero'
const favoritos = ref([])
const counter = ref(0)

const isAddDisabled = computed(() => {
  const numero = favoritos.value.find(favorito => favorito === counter.value)
  return  numero || numero === 0;
})

const classCounter = computed(() => {
  return counter.value < 0 ? 'numberRed' : (counter.value === 0 ? 'numberZero' : 'numberGreen');
})

const modify = (type) => {
  type === 0 ? counter.value++: (type === 1 ? counter.value-- : (type === 2 ? counter.value = 0 : counter.value = counter.value))
}

const addFavorito = () => {
  favoritos.value.push(counter.value);
}

</script>

<template>
  <div class="container text-center mt-5">
    <h1>Hola {{ name.toUpperCase() }}!</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="modify(0)" class="btn btn-success">Aumentar</button>
      <br>
      <button @click="modify(1)" class="btn btn-danger">Decrementar</button>
      <br>
      <button @click="modify(2)" class="btn btn-secondary">Resetear</button>
      <br>
      <button @click="addFavorito()" :disabled="isAddDisabled" class="btn btn-primary">Añadir favorito</button>
    </div>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(numeroFavorito, index) in favoritos" :key="numeroFavorito">
          {{ numeroFavorito }}
      </li>
    </ul>
  </div>
</template>

<style>
  h1 {
    color: red;
  }

  .numberRed{
    color: red;
  }

  .numberZero{
    color: blue;
  }

  .numberGreen{
    color: green;
  }

</style>
