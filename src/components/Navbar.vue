<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
      <a class="navbar-brand fw-bold" href="#">DoyanJajan</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav me-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/" >Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/foods" >Foods</router-link>
          </li>
        </ul>
        <ul class="navbar-nav ms-auto">
          <li class="nav-item">
            <router-link class="nav-link position-relative" to="/">
              <!-- Keranjang -->
              <img src="https://img.icons8.com/external-pixer-icons-pack-dmitry-mirolyubov/44/000000/external-cart-retail-pixer-icons-pack-dmitry-mirolyubov.png"/>
              <span class="position-absolute start-100 translate-middle badge rounded-pill bg-danger">
                {{ totalOrder.length }}
              </span>
            </router-link>
            <!-- <button type="button" class="btn btn-primary position-relative">
              Inbox
              <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
                99+
                <span class="visually-hidden">unread messages</span>
              </span>
            </button> -->
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from "axios";

export default {
  name: "Navbar",
  data() {
    return {
      totalOrder: {}
    }
  },
  methods: {
    setTotalOrder(data){
      this.totalOrder = data;
    }
  },
  mounted() {
    axios
      .get("http://localhost:3000/carts")
      .then((res) => this.setTotalOrder(res.data))
      .catch((err) => console.log(err));
  },
}
</script>

<style>

</style>