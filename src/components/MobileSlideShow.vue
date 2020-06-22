<template>
  <v-dialog :value="true" @input="$root.$emit('SLIDE_SHOW_CLOSED')">
    <v-sheet
      class="mx-auto"
      elevation="2"
    >
      <v-row justify="center">
        <v-col v-for="n in images.length" :key="n" cols="8" md="5">
          <div class="overline text-center font-weight-medium">-- {{ n >= 10 ? n : '0'+n }} --</div>
          <v-img
            :src="images[n-1]"
            _class="ma-2"
            _height="500" _width="300" contain/>
        </v-col>
      </v-row>
    </v-sheet>
  </v-dialog>
</template>

<script>
export default {
  name: 'MobileSlideShow',

  props: ['images']
}
</script>