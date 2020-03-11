<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
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
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Ultimate License Key Generator</span>
      </v-btn>
    </v-app-bar>

    <v-content>
      <Keys/>
    </v-content>
  </v-app>
</template>

<script>
import Keys from './components/Keys';

export default {
  name: 'App',

  components: {
    Keys,
  },

  data: () => ({
    //
  }),
};
</script>
