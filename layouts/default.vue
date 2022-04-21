<template>
  <v-app>
    <v-main class="py-15 myApp">
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout'
}
</script>

<style>
.myApp {
  background: 
    linear-gradient(135deg, red 13%, orange 47%, cyan)
}
</style>