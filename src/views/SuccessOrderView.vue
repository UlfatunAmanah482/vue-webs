<template>
  <section>
    <Navbar />
    <div class="container">
      <div class="row justify-content-center mt-5">
        <div class="col text-center">
          <img
            src="../assets/images/img-success.png"
            alt="success"
            width="300"
          />
          <h2><strong>Sukses!!</strong></h2>
          <h4>Pesanan Anda segera diproses, <br> Mohon ditunggu</h4>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Navbar from "@/components/Navbar.vue";

export default {
  name: "HomeView",
  components: {
    Navbar,
  },
}
</script>

<style>

</style>