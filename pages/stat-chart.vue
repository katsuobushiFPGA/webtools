<template>
  <v-row>
    <v-overlay :value="loading">
      <v-progress-circular indeterminate size="64" />
    </v-overlay>
    <v-row>
      <v-col class="text-center">
        <pie-chart :chart-data="chartData" :width="width" :height="height" />
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
  name: 'StatChart',
  components: { pieChart },
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
      },
      chartData: {
        // 凡例とツールチップに表示するラベル
        labels: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
        // 表示するデータ
        datasets: [
          {
            data: [10, 15, 6, 22, 11, 49, 32],
            backgroundColor: ['#f87979', '#aa4c8f', '#38b48b', '#006e54', '#c1e4e9', '#89c3eb', '#c3d825']
          }
        ]
      },
      height: window.innerHeight / 20,
      width: window.innerWidth / 20
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
