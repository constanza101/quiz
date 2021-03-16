<template>
  <v-app>
    <v-app-bar
      app
      color="#000"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />


      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/constanza101/quiz"
        target="_blank"
        text
      >
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
  name: 'App',

  components: {
    // HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
