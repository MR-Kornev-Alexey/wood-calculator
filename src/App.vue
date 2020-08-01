<template>
  <v-app>
    <v-app-bar app color="#4b1b85" dark>
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
      <h2 class="ml-4">Расчет займа</h2>
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-main>
      <vFinanceCalc />
    </v-main>
  </v-app>
</template>

<script>
import vFinanceCalc from "./components/v-finance-calc";

export default {
  name: "App",

  components: {
    vFinanceCalc
  },

  data: () => ({
    //
  })
};
</script>
