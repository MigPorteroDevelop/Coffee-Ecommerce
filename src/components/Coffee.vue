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

const emit = defineEmits(['add-to-cart']);

// Check if the product is in the cart
const isInCart = computed(() => {
  return props.cart.some(item => item.id === props.coffee.id);
});
</script>

<template>
  <div class="container col-md-6 col-lg-4 my-4 row align-items-stretch py-2">
    <div class="col-4 card-container">
      <img class="img-fluid" :src="'/img/' + coffee.image + '.jpg'" :alt="'img coffee' + coffee.name">
    </div>
    <div class="col-8 card-container">
      <div class="card-content">
        <h3 class="text-black fs-4 fw-bold text-uppercase">{{ coffee.name }}</h3>
        <p>{{ coffee.description }}</p>
        <p class="fw-black text-primary fs-4">{{ coffee.price }} €</p>
      </div>
      <div v-if="!isInCart" class="card-footer">
        <button type="button" class="btn btn-dark w-100" @click="$emit('add-to-cart', coffee)">Add to Cart</button>
      </div>
      <div v-else class="card-footer">
        <button class="btn btn-danger w-100">Added</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.btn-danger {
  cursor: auto;
}
.card-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}

.card-container img {
  width: 100%;
  height: auto;
}
.card-content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}

.card-footer {
  margin-top: auto;
}
</style>