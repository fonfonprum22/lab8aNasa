<template>
  <v-app>
    <v-app-bar app color="yellow lighten-1" dark>
      <div class="d-flex align-center">
        <h1  class="black--text">NASA</h1>
      </div>
    </v-app-bar>

    <v-main>
      <HelloWorld />
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
