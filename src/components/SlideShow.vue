<template>
  <div>
    <v-dialog :value="true" @input="$root.$emit('SLIDE_SHOW_CLOSED')">
      <v-sheet
        class="mx-auto"
        elevation="8"
      >
        <div _v-if="!slideModel" class="caption text-center font-weight-medium pt-1">Click on image to enlarge</div>
        <v-slide-group
          v-model="slideModel"
          class="pa-4 pt-0"
          center-active
          _mandatory
          :show-arrows="true"
          next-icon="mdi-hand-pointing-right"
          prev-icon="mdi-hand-pointing-left"
        >
          <!-- <template v-slot:next>
            <v-icon color="orange" large>mdi-hand-pointing-right</v-icon>
          </template>

          <template v-slot:prev>
            <v-icon color="orange" large>mdi-hand-pointing-left</v-icon>
          </template> -->

          <v-slide-item
            v-for="n in images.length"
            :key="n"
            v-slot:default="{ active, toggle }"
          >
            <v-sheet
              class="ma-2"
              :outlined="active ? true : false"
              :shaped="active ? true : false"
              :elevation="active ? 4 : 0"
              @click="toggle">
              <v-img
                @click="activeImageIndex=n-1"
                :src="images[n-1]"
                class="ma-2"
                height="500" width="300" contain/>
              <div class="overline text-center font-weight-medium">-- {{ n >= 10 ? n : '0'+n }} --</div>
            </v-sheet>
          </v-slide-item>
        </v-slide-group>
      </v-sheet>
    </v-dialog>

    <v-dialog v-model="subDialogModel" max-width="420">
      <v-img :src="images[slideModel]" max-width="420" contain/>
    </v-dialog>
  </div>
</template>

<script>
export default {
  name: 'SlideShow',

  props: ['images'],

  data: () => ({
    subDialogModel: false,
    slideModel: null,
    activeImageIndex: null
  }),

  watch: {
    slideModel: function (value) {
      if (value != undefined) {
        this.subDialogModel = true
      } else {
        this.subDialogModel = false
      }
    }
  },

  methods: {
  }
}
</script>
