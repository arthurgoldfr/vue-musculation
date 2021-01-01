<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
      >
      <div class="links">
        <router-link class="router" tag="a" to="/">Home</router-link>  |  
        <router-link class="router" tag="a" to="/About">About</router-link>
      </div>
    </v-app-bar>
    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    //
  }),
};
</script>

<style>
.v-application a.router {
  color: white;
}
.links {
  margin: 0 auto;
}
</style>
