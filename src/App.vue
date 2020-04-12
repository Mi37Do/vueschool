<template>
  <v-app>
    <v-card
            color="grey lighten-4"
            flat
            height="200px"
            tile
    >
      <v-toolbar dense>
        <router-link to="/" style="margin-right: 20px">hoe</router-link>
        <router-link to="/about">about</router-link>

        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-heart</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </v-toolbar>
    </v-card>
    <v-content>
      <router-view></router-view>
    </v-content>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  components: {

  },

  data: () => ({
    //
  }),
};
</script>
