<script setup>
import { ref, onMounted, watch } from 'vue';
import { db } from './data/coffee.js';
import Coffee from './components/Coffee.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue'

const coffees = ref([]);
const cart = ref([]);
const coffee = ref({});

watch(cart, () => {
  saveLocalStorage();
}, {
  //access every atribute of cart
  deep:true
})

onMounted(() => {
  coffees.value = db;
  coffee.value = db[3];

  //persistence
  const cartStorage = localStorage.getItem('cart');

  if (cartStorage) {
    cart.value = JSON.parse(cartStorage)
  }
})

//persistence
const saveLocalStorage = () => {
  localStorage.setItem('cart', JSON.stringify(cart.value))
}

const addToCart = (coffee) => {
  const existCart = cart.value.findIndex(product => product.id === coffee.id)

  if (existCart >= 0) {
    //don't use id from db, use position in array
    cart.value[existCart].quantity++
  } else {
    coffee.quantity = 1;
    cart.value.push(coffee);
  }
}

const deleteProduct = (id) => {
  cart.value = cart.value.filter(product => product.id !== id)
}

const emptyCart = () => {
  cart.value = []
}

const incrementQuantity = (id) => {
  const index = cart.value.findIndex(product => product.id === id)
  if (cart.value[index].quantity >= 10) return
  cart.value[index].quantity++
}

const decrementQuantity = (id) => {
  const index = cart.value.findIndex(product => product.id === id)
  if (cart.value[index].quantity <= 1) return
  cart.value[index].quantity--
}
</script>

<template>
  <Header 
  :cart="cart" 
  :coffee="coffee" 
  @increment-quantity="incrementQuantity" 
  @decrement-quantity="decrementQuantity"
  @add-to-cart="addToCart" 
  @delete-product="deleteProduct" @empty-cart="emptyCart" />

  <main class="container-xl">
    <h2 class="text-center py-5">Our Collection</h2>
    <!-- COFFEE -->
    <div class="row">
      <Coffee v-for="coffee in coffees" 
      :key="coffee.id"
      :cart="cart"
      :coffee="coffee" 
      @add-to-cart="addToCart" />
    </div>
  </main>

  <Footer />
</template>
