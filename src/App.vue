<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Whatsapp</span>
      </v-toolbar-title>
    </v-toolbar>

    <v-content>
      <MainPage/>
    </v-content>
  </v-app>
</template>

<script>
import MainPage from "./components/MainPage";

export default {
  name: "App",
  components: {
    MainPage
  },
  data() {
    return {
      //
    };
  }
};
</script>
