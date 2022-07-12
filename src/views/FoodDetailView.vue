<template>
  <section>
    <Navbar />
    <div class="container">
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark text-decoration-none"
                  >Home</router-link
                >
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark text-decoration-none"
                  >Foods</router-link
                >
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Food Order
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col-md-6">
          <img
            :src="'../assets/images/' + product.gambar"
            alt="..."
            class="img-fluid shadow"
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>
            Harga: <strong>{{ product.harga }}</strong>
          </h4>
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group mb-3">
              <label for="jumlah_pesanan" class="form-label"
                >Jumlah Pesanan</label
              >
              <input
                type="number"
                class="form-control"
                v-model="order.jumlah_pemesanan"
              />
            </div>
            <div class="form-group mb-3">
              <label for="keterangan" class="form-label">Keterangan</label>
              <textarea
                class="form-control"
                placeholder="Keterangan misal: pedas, nasi setengah, dll"
                v-model="order.keterangan"
              ></textarea>
            </div>
            <button type="submit" class="btn btn-success" @click="setOrder">
              <img
                src="https://img.icons8.com/material-outlined/24/FFFFFF/shopping-cart--v1.png"
              />
              Pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "HomeView",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {},
      order: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    setOrder() {
      this.order.products = this.product;
      axios
        .post("http://localhost:3000/carts", this.order)
        .then(() => {
          this.$router.push({ path: "/cart" })
        })
        .catch((err) => console.log(err));
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((res) => {
        console.log(res.data);
        this.setProduct(res.data);
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style>
</style>