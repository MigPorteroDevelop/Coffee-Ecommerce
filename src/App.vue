<script setup>
import { ref, reactive, onMounted } from 'vue';
import { db } from './data/guitars';
import Guitar from './components/Guitar.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue'

const guitars = ref([]);
const cart = ref([]);

onMounted(() => {
  guitars.value = db;
})

const addToCart = (guitar) => {
  const existCart = cart.value.findIndex(product => product.id === guitar.id)

  if (existCart >= 0) {
    //don't use id from db, use position in array
    cart.value[existCart].quantity++
  } else {
    guitar.quantity = 1;
    cart.value.push(guitar);
  }
}

const incrementQuantity = (id) => {
  const index = cart.value.findIndex(product => product.id === id)
  if(cart.value[index].quantity >= 10) return
  cart.value[index].quantity++
}

const decrementQuantity = (id) => {
  const index = cart.value.findIndex(product => product.id === id)
  if(cart.value[index].quantity <= 1) return
  cart.value[index].quantity--
}

defineEmits(['increment-quantity', 'decrement-quantity'])
</script>

<template>
  <Header 
  :cart="cart" 
  @increment-quantity="incrementQuantity" 
  @decrement-quantity="decrementQuantity" />

  <main class="container-xl">
    <h2 class="text-center py-5">Our Collection</h2>
    <!-- GUITAR -->
    <div class="row">
      <Guitar 
      v-for="guitar in guitars" 
      :guitar="guitar" 
      @add-to-cart="addToCart" />
    </div>
  </main>

  <Footer />
</template>
