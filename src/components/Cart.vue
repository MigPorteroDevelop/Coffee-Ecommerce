<script setup>
import { computed } from 'vue';

const props = defineProps({
  cart: {
    type: Array,
    required: true
  },
  coffee: {
    type: Object,
    required: true
  }
});
const emit = defineEmits(['increment-quantity', 'decrement-quantity', 'delete-product', 'empty-cart']);

const totalPayment = computed(() => {
  return props.cart.reduce((total, product) => total + (product.quantity * product.price), 0);
});
</script>

<template>
  <nav class="col-md-6 mt-5 d-flex align-items-start justify-content-end">
    <div class=cart>
      <img class="img-fluid" src="/img/cart.png" alt="imagen cart" />

      <div id=cart class="bg-white pl-2">
        <p v-if="cart.length === 0" class="text-center m-0 ">CART IS EMPTY</p>
        <div v-else>
          <table class="w-100 table">
            <thead>
              <tr>
                <th>Image</th>
                <th>Name</th>
                <th>Price</th>
                <th>Quantity</th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="product in cart">
                <td>
                  <img class="img-fluid" :src="'/img/' + product.image + '.jpg'" :alt="'coffee img' + product.name">
                </td>
                <td>{{ product.name }}</td>
                <td class="fw-bold">
                  {{ product.price }}€
                </td>
                <td class="flex align-items-start gap-4">
                  <button @click="$emit('decrement-quantity', product.id)" type="button" class="btn btn-dark">
                    -
                  </button>
                  {{ product.quantity }}
                  <button @click="$emit('increment-quantity', product.id)" type="button" class="btn btn-dark">
                    +
                  </button>
                </td>
                <td>
                  <button class="btn btn-danger" type="button" @click="$emit('delete-product', product.id)">
                    X
                  </button>
                </td>
              </tr>
            </tbody>
          </table>

          <p class="text-end">Total payable: <span class="fw-bold">{{ totalPayment }} €</span></p>
          <button class="btn btn-dark w-100 mt-3 p-2" @click="$emit('empty-cart')">Empty Cart</button>
        </div>
      </div>
    </div>
  </nav>
</template>