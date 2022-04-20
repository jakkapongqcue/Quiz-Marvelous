<template>
  <v-app class="bg-color">
    <Navbar />
    <v-main>
      <Nuxt />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {}
  },
}
</script>

<style scoped>
.bg-color {
  background-color: #f6f6fa;
  color: #000000;
}
</style>
