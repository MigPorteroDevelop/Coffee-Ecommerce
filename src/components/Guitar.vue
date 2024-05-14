<script setup>
const props = defineProps({
  guitar: {
    type: Object,
    required: true
  }
})

defineEmits(['add-to-cart'])
</script>

<template>
  <div class="container col-md-6 col-lg-4 my-4 row align-items-stretch py-2">
    <div class="col-4 card-container">
      <img class="img-fluid" 
      :src="'/img/' + guitar.image + '.jpg'" 
      :alt="'img guitar' + guitar.name">
    </div>
    <div class="col-8 card-container">
      <div class="card-content">
        <h3 class="text-black fs-4 fw-bold text-uppercase">{{ guitar.name }}</h3>
        <p>{{ guitar.description }}</p>
        <p class="fw-black text-primary fs-3">{{ guitar.price }} €</p>
      </div>
      <div class="card-footer">
        <button type="button" class="btn btn-dark w-100" 
        @click="$emit('add-to-cart', guitar)">Add to Cart</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
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