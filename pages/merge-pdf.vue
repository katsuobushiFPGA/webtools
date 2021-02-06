<template>
  <v-row>
    <v-col class="text-center">
      <dropzone id="dropzone" ref="el" :options="options" :destroy-dropzone="true" />
    </v-col>
  </v-row>
</template>
<script>
import Dropzone from 'nuxt-dropzone'
import 'nuxt-dropzone/dropzone.css'
export default {
  components: {
    Dropzone
  },
  data() {
    return {
      options: {
        url: 'http://httpbin.org/anything'
      }
    }
  }
}
</script>
