<template>
  <v-app>
    <v-app-bar app
      _absolute
      color="dark"
      dark
      shrink-on-scroll
      prominent
      src="https://picsum.photos/900/300?random"
      fade-img-on-scroll
      scroll-target="#scrolling-target"
      scroll-threshold="500"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(65, 120, 163,.7), rgba(25,32,72,.7)"
        ></v-img>
      </template>

      <!-- <v-app-bar-nav-icon></v-app-bar-nav-icon> -->
      <v-avatar _size="48" class="mr-2">
        <img src="https://material.io/resources/icons/static/ic_material_192px_light.svg">
      </v-avatar>

      <v-toolbar-title class="text-h6 text-sm-h5">Material Design Showcase</v-toolbar-title>

      <v-spacer/>
      <v-btn
        href="https://materialdesignkit.com"
        target="_blank"
        text
        class="hidden-xs-only">
        <span class="mr-2">Buy</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main id="scrolling-target" class="grey lighten-4">
      <v-container fluid>
        <v-row>
          <v-col v-for="n in templates.length" :key="n" cols="12" sm="6" md="4" lg="3">
            <v-skeleton-loader
              :loading="skeletonLoading"
              transition="scale-transition"
              class="mx-auto"
              max-width="300"
              type="card">
              <ShowCase :templateItem="templates[n-1]"/>
            </v-skeleton-loader>
          </v-col>
        </v-row>
      </v-container>
    </v-main>

    <v-footer app class="grey darken-3 white--text">
      <div class="ml-3 text-caption text-sm-body-2">
          Made with <v-icon class="red--text" style="vertical-align: middle;" _large>mdi-heart-outline</v-icon>
          by <a class="white--text" href="https://vuetifyjs.com" target="_blank">Vuetify</a>
          and <a class="white--text" href="https://github.com/hoangtuan151" target="_blank">Author</a>
      </div>
      <v-spacer/>
      <div class="mr-3 hidden-xs-only">
          Copyright &copy; 2020
      </div>
    </v-footer>

  </v-app>
</template>

<script>
import ShowCase from '@/components/ShowCase';
import axios from 'axios'

export default {
  name: 'App',

  components: {
    ShowCase,
  },

  data: () => ({
    skeletonLoading: true,
    templates: []
  }),

  async created () {
    setTimeout(() => {
      this.skeletonLoading = false
    }, 1500);

    let resp = await axios.get('/material-app-design-showcase/data.json')
    if (resp.data) {
      this.templates = resp.data
    }
  }
};
</script>
