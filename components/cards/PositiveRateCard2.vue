<template>
  <v-col cols="12" md="6" class="DataCard">
    <time-bar-chart
      :title="
        $t(
          '参考：『東京都の』陽性率（直近3日平均：直近3日総陽性者数/直近3日総検査人数 x 100[%]）'
        )
      "
      :title-id="'positive-rate2'"
      :chart-id="'time-bar-chart-patients'"
      :chart-data="patientsGraph"
      :date="Data.patients.date"
      :unit="$t('%')"
    />
  </v-col>
</template>

<i18n>
{
  "ja": {
    "陽性患者数": "陽性患者数",
    "人": "人"
  },
  "en": {
    "陽性患者数": "Number of confirmed cases",
    "人": "persons"
  },
  "zh-cn": {
    "陽性患者数": "确诊人数",
    "人": "人"
  },
  "zh-tw": {
    "陽性患者数": "確診人數",
    "人": "人"
  },
  "ko": {
    "陽性患者数": "확진자 수",
    "人": "인"
  },
  "ja-basic": {
    "陽性患者数": "びょうきの ひとの かず",
    "人": "にん"
  }
}
</i18n>

<script>
// import Data from '@/data/positiverate3.json'//origin
import Data from '@/data/positiverate3-tokyo.json'
import formatGraph from '@/utils/formatGraph'
import TimeBarChart from '@/components/TimeBarChart3.vue'

export default {
  components: {
    TimeBarChart
  },
  data() {
    // 感染者数グラフ
    const patientsGraph = formatGraph(Data.patients_summary.data)
    // const patientsGraph2 = formatGraph(Data2.patients_summary.data)

    const data = {
      Data,
      patientsGraph
    }
    return data
  }
}
</script>
