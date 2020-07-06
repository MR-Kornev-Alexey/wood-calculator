<template>
  <v-app>
    <v-app-bar app color="primary" dark>
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
      <h2 class="ml-4">Калькулятор пилометериала</h2>
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-main>
      <v-wood-calc />
    </v-main>
  </v-app>
</template>

<script>
import vWoodCalc from "./components/v-wood-calc";

export default {
  name: "App",

  components: {
    vWoodCalc
  },

  data: () => ({
    //
  })
};
</script>
