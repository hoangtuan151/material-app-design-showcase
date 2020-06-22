<template>
  <div>
    <v-hover v-slot:default="{ hover }">
      <v-card class="mx-auto" max-width="350" :elevation="hover ? 12 : 2" @click="cardClicked">
        <v-img :src="`https://source.unsplash.com/350x200/?${templateItem.title}`" _height="450px" contain></v-img>

        <v-card-title>
          {{ templateItem.title }}
        </v-card-title>

        <v-card-subtitle>
          {{ templateItem.desc }}
        </v-card-subtitle>
      </v-card>
    </v-hover>


    <SlideShow v-if="showSlideShow && $vuetify.breakpoint.lgAndUp" :images="templateItem.imgs" />
    <MobileSlideShow v-if="showSlideShow && $vuetify.breakpoint.mdAndDown" :images="templateItem.imgs" />
  </div>
</template>

<script>
import SlideShow from '@/components/SlideShow'
import MobileSlideShow from '@/components/MobileSlideShow'

export default {
  name: 'ShowCase',

  components: {
    SlideShow,
    MobileSlideShow
  },

  props: ['templateItem'],

  data: () => ({
    showSlideShow: false
  }),

  computed: {
    imgUrl () {
      return `https://picsum.photos/350/200?random=${new Date().getTime()}`
    }
  },

  created () {
    console.log('ShowCase::created()')
    this.$root.$on('SLIDE_SHOW_CLOSED', () =>{
      this.showSlideShow = false
    })
  },

  methods: {
    cardClicked () {
      this.showSlideShow = true
    }
  }
}
</script>
