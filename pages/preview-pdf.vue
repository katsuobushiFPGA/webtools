<template>
  <v-row>
    <v-col class="text-center">
      <input type="file" accept="application/pdf" @change="onFileChange($event)" />
      <span>PDFファイルを選択するとプレビューをします。</span>
      <pdf
        :src="pdf_url"
        :page="previewPdf.page"
        @num-pages="previewPdf.pageCount = $event"
        @page-loaded="previewPdf.currentPage = $event"
      />
      <v-row>
        <v-col>
          <v-slider v-model="previewPdf.page" hint="slide pdf page." :max="previewPdf.pageCount" :min="0" />
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <button type="button" :disabled="previewPdf.currentPage <= 1" @click="prev()">Prev</button>
        </v-col>
        <v-col>
          <button type="button" :disabled="previewPdf.currentPage > previewPdf.pageCount" @click="next()">Next</button>
        </v-col>
        <v-col>{{ previewPdf.currentPage }} / {{ previewPdf.pageCount }}</v-col>
      </v-row>
    </v-col>
  </v-row>
</template>
<script>
import pdf from 'vue-pdf'
export default {
  components: { pdf },
  data() {
    return {
      pdf_file: null,
      pdf_url: null,
      previewPdf: {
        page: 1,
        currentPage: 0,
        pageCount: 0
      }
    }
  },
  methods: {
    onFileChange(e) {
      const file = e.target.files[0]
      this.pdf_file = file
      this.pdf_url = window.URL.createObjectURL(file)
    },
    prev() {
      if (this.previewPdf.currentPage > 1) {
        this.previewPdf.page--
      }
    },
    next() {
      if (this.previewPdf.currentPage < this.previewPdf.pageCount) {
        this.previewPdf.page++
      }
    }
  }
}
</script>
