<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { Director, ConcreteBuilder1, type Product } from '@/classes/Form'
import TheFormBuilder from './TheFormBuilder.vue';
let director: Director | null = null;
let fields = ref([] as Product[]);

onMounted(() => {
  director = new Director();
})

const constructorBasic = (director: Director) => {
  const builder = new ConcreteBuilder1();
  director.setBuilder(builder);

  director.buildMinimalViableProduct();
  return builder.getProduct().listParts();
}

const constructorFull = (director: Director) => {
  const builder = new ConcreteBuilder1();
  director.setBuilder(builder);

  director.buildFullFeaturedProduct();
  return builder.getProduct().listParts();
}

const showBasicForm = () => {
  if(director === null) return;
  fields.value = constructorBasic(director);
}

const showFullForm = () => {
  console.log('Show Full Form');
  if(director === null) return;
  fields.value = constructorFull(director);
}
</script>

<template>
  <div class="container">
    <h1>Builder</h1>
    <button @click="showBasicForm">Show Basic Form</button>
    <button @click="showFullForm">Show Full Form</button>
    <form>
      <TheFormBuilder :fields="fields" v-if="fields.length !== 0"/>
      <button type="submit">Enviar</button>
    </form>
  </div>
</template>
