<template>
  <div class="card shadow card-product">
    <img :src=" '/assets/images/' + product.gambar " class="card-img-top" alt="...">
    <div class="card-body">
      <h5 class="card-title">{{ product.nama }}</h5>
      <p class="card-text">Harga: {{ product.harga }}</p>
      <router-link :to="'foods/' + product.id" class="btn btn-success">
        <img src="https://img.icons8.com/material-outlined/24/FFFFFF/shopping-cart--v1.png"/>
        Pesan
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["product"]
}
</script>

<style>

</style>