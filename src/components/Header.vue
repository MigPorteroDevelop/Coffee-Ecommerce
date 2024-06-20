<script setup>
import { computed } from 'vue';
import Cart from './Cart.vue';

const props = defineProps({
  cart: {
    type: Array,
    required: true
  },
  coffee: {
    type: Object,
    required: true
  }
})
defineEmits(['increment-quantity', 'decrement-quantity', 'add-to-cart', 'delete-product', 'empty-cart'])

const isInCart = computed(() => {
  return props.cart.some(item => item.id === props.coffee.id);
});
</script>

<template>
  <header class="py-5 px-5 header">
    <div class="container-xl">
      <div class="row justify-content-center justify-content-md-between">
        <div class="col-8 col-md-3">
          <a href="index.html">
            <img class="img-fluid" src="/img/logo.png" alt="img logo">
          </a>
        </div>
        <Cart 
          :cart="cart" 
          :coffee="coffee"
          @increment-quantity="$emit('increment-quantity', $event)" 
          @decrement-quantity="$emit('decrement-quantity', $event)"
          @add-to-cart="$emit('add-to-cart', $event)" 
          @delete-product="$emit('delete-product', $event)" 
          @empty-cart="$emit('empty-cart', $event)" 
        />
      </div>

      <div class="row mt-5">
        <div class="col-md-6 text-center text-md-start pt-5">
          <h1 class="display-2 fw-bold">{{ coffee.name }}</h1>
          <p class="mt-5 fs-5 text-white">{{ coffee.description }}</p>
          <p class="text-primary fs-1 fw-black">{{ coffee.price }} €</p>
          <div v-if="!isInCart">
            <button @click="$emit('add-to-cart', coffee)" type="button"
              class="btn fs-4 bg-primary text-white py-2 px-5">Add to Cart</button>
          </div>
          <div v-else>
            <button class="btn fs-4 bg-primary text-white py-2 px-5">ADDED</button>
          </div>
        </div>
      </div>
      <img class="header-coffee" src="/img/header_coffee.png" alt="image header">
    </div>
  </header>
</template>


