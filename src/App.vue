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
          src="../public/assets/images/shopware_logo_blue.svg"
          transition="scale-transition"
          width="200"
        />
      </div>
    </v-app-bar>

    <v-content>
      <List/>
    </v-content>
  </v-app>
</template>

<script>
import List from './components/List';

export default {
  name: 'App',

  components: {
    List,
  },

  data: () => ({
    //
  }),
};
</script>
