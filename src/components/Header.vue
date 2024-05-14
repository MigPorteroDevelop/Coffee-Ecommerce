<script setup>
const props = defineProps({
  cart: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <header class="py-5 header">
    <div class="container-xl">
      <div class="row justify-content-center justify-content-md-between">
        <div class="col-8 col-md-3">
          <a href="index.html">
            <img class="img-fluid" src="/img/logo.png" alt="img logo">
          </a>
        </div>
        <nav class="col-md-6 a mt-5 d-flex align-items-start justify-content-end">
          <div class=cart>
            <img class="img-fluid" src="/img/cart.png" alt="imagen cart" />

            <div id=cart class="bg-white p-3">
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
                        <img class="img-fluid" 
                        :src="'/img/' + product.image + '.jpg'"
                        :alt="'guitar img' + product.name">
                      </td>
                      <td>{{ product.name }}</td>
                      <td class="fw-bold">
                        {{ product.price }}
                      </td>
                      <td class="flex align-items-start gap-4">
                        <button type="button" class="btn btn-dark">
                          -
                        </button>
                        {{ product.quantity }}
                        <button type="button" class="btn btn-dark">
                          +
                        </button>
                      </td>
                      <td>
                        <button class="btn btn-danger" type="button">
                          X
                        </button>
                      </td>
                    </tr>
                  </tbody>
                </table>

                <p class="text-end">Total payable: <span class="fw-bold">$899</span></p>
                <button class="btn btn-dark w-100 mt-3 p-2">Empty Cart</button>
              </div>
            </div>
          </div>
        </nav>
      </div>

      <div class="row mt-5">
        <div class="col-md-6 text-center text-md-start pt-5">
          <h1 class="display-2 fw-bold">VAI model</h1>
          <p class="mt-5 fs-5 text-white">Lorem ipsum dolor sit amet consectetur adipisicing elit. Temporibus,
            possimus
            quibusdam dolor nemo velit quo, fuga omnis, iure molestias optio tempore sint at ipsa dolorum
            odio
            exercitationem eos inventore odit.</p>
          <p class="text-primary fs-1 fw-black">$399</p>
          <button type="button" class="btn fs-4 bg-primary text-white py-2 px-5">Add to Cart</button>
        </div>
      </div>
    </div>

    <img class="header-guitarra" src="" alt="image header">
  </header>

</template>