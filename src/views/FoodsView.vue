<template>
  <div class="home">
    <Navbar />
    <h3>Foods</h3>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'

export default {
  name: 'FoodsView',
  components: {
    Navbar
  }
}
</script>
