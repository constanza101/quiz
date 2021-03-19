<template>
  <v-app>
    <v-app-bar app color="#000" dark>
      <div class="d-flex align-center">
        <v-img
          @click="home"
          alt="Vuetify Logo"
          class="shrink mr-5"
          contain
          :src="require('./assets/printful-logo.png')"
          transition="scale-transition"
          width="40"
          style="cursor: pointer"
        />
      </div>

      <span> Constanza Díaz</span>

      <v-spacer></v-spacer>

      <v-btn href="https://github.com/constanza101/quiz" target="_blank" text>
        <v-icon>mdi-github</v-icon>
        <span class="mr-2"></span>
      </v-btn>
    </v-app-bar>

    <v-main>
      <!-- <HelloWorld/> -->

      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';

export default {
  name: "App",

  components: {
    // HelloWorld,
  },

  data: () => ({
    //
  }),
  methods: {
    home() {
      this.$router.push({
        name: "Home",
      });
    },
  },
};
</script>
