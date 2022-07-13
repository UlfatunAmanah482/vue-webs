<template>
  <section>
    <Navbar :updateCart="carts" />
    <div class="container">
      <div class="row mt-4">
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
              <li class="breadcrumb-item active" aria-current="page">Cart</li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col">
          <table class="table">
            <thead>
              <tr align="center">
                <th scope="col">No</th>
                <th scope="col">Foto</th>
                <th scope="col">Makanan</th>
                <th scope="col">Keterangan</th>
                <th scope="col">Jumlah</th>
                <th scope="col">Harga</th>
                <th scope="col">Total Harga</th>
                <th scope="col">Hapus</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(cart, index) in carts" :key="cart.id" align="center">
                <th>{{ index + 1 }}</th>
                <td>
                  <img
                    :src="'../assets/images/' + cart.products.gambar"
                    alt="..."
                    class="img-fluid shadow"
                    width="250"
                  />
                </td>
                <td>
                  <strong>{{ cart.products.nama }}</strong>
                </td>
                <td>{{ cart.keterangan ? cart.keterangan : "-" }}</td>
                <td>{{ cart.jumlah_pemesanan }}</td>
                <td>Rp. {{ cart.products.harga }}</td>
                <td>
                  <strong>Rp. {{ cart.products.harga * cart.jumlah_pemesanan }}</strong>
                </td>
                <td>
                  <img src="https://img.icons8.com/ios-glyphs/30/E74C3C/trash--v1.png" @click="deleteItem(cart.id)" style="cursor: pointer" />
                </td>
              </tr>

              <tr>
                <td colspan="6"  align="right">
                  <strong>Total Harga:</strong>
                </td>
                <td align="center">
                  <strong>Rp. {{ totalHarga }}</strong>
                </td>
                <td></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "CartView",
  components: {
    Navbar,
  },
  data() {
    return {
      carts: []
    }
  },
  methods: {
    setCarts(data){
      this.carts = data;
    },
    deleteItem(id){
      axios
        .delete("http://localhost:3000/carts/"+id)
        .then((res) => console.log("success delete item"))
        .catch((err) => console.log(err))

      axios
        .get("http://localhost:3000/carts")
        .then((res) => this.setCarts(res.data))
        .catch((err) => console.log(err));
    }
  },
  mounted() {
    axios
      .get("http://localhost:3000/carts")
      .then((res) => this.setCarts(res.data))
      .catch((err) => console.log(err));
  },
  computed: {
    totalHarga(){
      return this.carts.reduce((items, data) => {
        return items + data.products.harga * data.jumlah_pemesanan
      }, 0)
    }
  }
};
</script>

<style>
</style>