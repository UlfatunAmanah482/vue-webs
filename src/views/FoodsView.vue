<template>
  <section>
    <Navbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h2>Daftar <strong>Makanan</strong></h2>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
            <input
              v-model="search"
              type="text"
              class="form-control"
              placeholder="Search Your Favorite Foods"
              aria-label="Cari"
              aria-describedby="basic-addon1"
              @keyup="searchFoods"
            />
            <span class="input-group-text" id="basic-addon1">
              <img
                src="https://img.icons8.com/ios-glyphs/30/000000/search--v1.png"
              />
            </span>
          </div>
        </div>
      </div>

      <div class="row mb-3">
        <div
          class="col-md-4 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/Navbar.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "FoodsView",
  components: {
    Navbar,
    CardProduct,
  },
  data() {
    return {
      products: [],
      search: ""
    };
  },
  methods: {
    setProducts(data) {
      this.products = data;
    },
    searchFoods() {
      axios
        .get("http://localhost:3000/products?q=" + this.search)
        .then((res) => this.setProducts(res.data))
        .catch((err) => console.log(err))
    }
  },
  mounted() {
    axios
      .get("http://localhost:3000/products")
      .then((res) => this.setProducts(res.data))
      .catch((err) => console.log(err));
  },
};
</script>
