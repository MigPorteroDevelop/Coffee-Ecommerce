<script setup>
import { ref, reactive, onMounted } from 'vue';
import { db } from './data/guitars';
import Guitar from './components/Guitar.vue';

const guitars = ref([]);

onMounted(() => {
  guitars.value = db;
})

</script>

<template>
  <header class="py-5 header">
    <div class="container-xl">
      <div class="row justify-content-center justify-content-md-between">
        <div class="col-8 col-md-3">
          <a href="index.html">
            <img class="img-fluid" src="/public/img/logo.png" alt="img logo">
          </a>
        </div>
        <nav class="col-md-6 a mt-5 d-flex align-items-start justify-content-end">
          <div class=cart>
            <img class="img-fluid" src="/public/img/cart.png" alt="imagen cart" />

            <div id=cart class="bg-white p-3">
              <p class="text-center">Cart is empty</p>
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
                  <tr>
                    <td>
                      <img class="img-fluid" src="/public/img/guitar_02.jpg" alt="img guitar">
                    </td>
                    <td>SRV</td>
                    <td class="fw-bold">
                      $299
                    </td>
                    <td class="flex align-items-start gap-4">
                      <button type="button" class="btn btn-dark">
                        -
                      </button>
                      1
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
        </nav>
      </div><!--.row-->

      <div class="row mt-5">
        <div class="col-md-6 text-center text-md-start pt-5">
          <h1 class="display-2 fw-bold">VAI model</h1>
          <p class="mt-5 fs-5 text-white">Lorem ipsum dolor sit amet consectetur adipisicing elit. Temporibus, possimus
            quibusdam dolor nemo velit quo, fuga omnis, iure molestias optio tempore sint at ipsa dolorum odio
            exercitationem eos inventore odit.</p>
          <p class="text-primary fs-1 fw-black">$399</p>
          <button type="button" class="btn fs-4 bg-primary text-white py-2 px-5">Add to Cart</button>
        </div>
      </div>
    </div>

    <img class="header-guitarra" src="/public/img/header_guitar.png" alt="image header">
  </header>

  <main class="container-xl">
    <h2 class="text-center py-5">Our Collection</h2>
    <!-- GUITAR -->
    <div class="row">
      <Guitar v-for="guitar in guitars" 
      :guitar="guitar" />
    </div>
  </main>


  <footer class="bg-dark mt-5 py-5">
    <div class="container-xl">
      <p class="text-white text-center fs-4 mt-4 m-md-0">DreamGuitar - All Rights Reserved</p>
    </div>
  </footer>
</template>

<style scoped></style>
