<template>
  <v-row>
    <v-overlay :value="loading">
      <v-progress-circular indeterminate size="64" />
    </v-overlay>
    <v-row>
      <v-col class="text-center">
        <pie-chart />
      </v-col>
    </v-row>
  </v-row>
</template>
<script>
import axios from 'axios'
import pieChart from '../components/PieChart'
const VERSION = '3.0'
const E_STAT_DATA_API_URL = `https://api.e-stat.go.jp/rest/${VERSION}/app/json/getStatsData?`
export default {
  components: pieChart,
  data() {
    return {
      loading: false,
      stat: {},
      params: {
        appId: process.env.E_STAT_APP_ID,
        lang: 'J',
        statsDataId: '0003286000',
        surveyYears: '201603',
        metaGetFlg: 'Y',
        cntGetFlg: 'N',
        explanationGetFlg: 'Y',
        annotationGetFlg: 'Y',
        sectionHeaderFlg: '1'
      }
    }
  },
  mounted() {
    this.get()
  },
  methods: {
    get() {
      this.loading = true
      const params = new URLSearchParams(this.params)
      const url = E_STAT_DATA_API_URL + params
      axios.get(url).then((response) => {
        this.stat = response
        setTimeout(() => {
          this.loading = false
        }, 1000)
      })
    }
  }
}
</script>
