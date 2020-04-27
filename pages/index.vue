<template>
  <div class="MainPage">
    <page-header
      :icon="headerItem.icon"
      :title="headerItem.title"
      :date="headerItem.date"
    />
    <whats-new class="mb-4" :items="newsItems" />
    <div class="EmergencyPosterBlock mb-4" align="center">
      <img class="EmergencyPosterImage" src="/emergency-poster.png" />
    </div>
    <static-info
      class="mb-4"
      :url="localePath('/flow')"
      :text="$t('自分や家族の症状に不安や心配があればまずは電話相談をどうぞ')"
      :btn-text="$t('相談の手順を見る')"
    />
    <v-row class="DataBlock">
      <tested-number-card />
      <confirmed-cases-number-card />
      <positive-rate-card />
      <positive-rate-card2 />
      <confirmed-cases-details-card />
      <confirmed-cases-attributes-card />
      <!--<telephone-advisory-reports-number-card />
      <consultation-desk-reports-number-card />
      <metro-card />
      <agency-card />-->
    </v-row>
    <static-info
      class="mb-4"
      :url="'https://stopcovid19.metro.tokyo.lg.jp/'"
      :text="$t('【緊急事態宣言発令中！】東京都公式サイト')"
      :btn-text="$t('Jump!')"
    />
    <static-info
      class="mb-4"
      :url="'https://stopcovid19-yamagata-unofficial.netlify.app/'"
      :text="$t('【近隣県（県北部）】山形県非公式サイト')"
      :btn-text="$t('Jump!')"
    />
    <static-info
      class="mb-4"
      :url="'https://fukushima-covid19.firebaseapp.com/'"
      :text="$t('【近隣県（阿賀野川の源流）】福島県非公式サイト')"
      :btn-text="$t('Jump!')"
    />
    <static-info
      class="mb-4"
      :url="'https://stopcovid19.pref.gunma.jp/'"
      :text="$t('【近隣県（関越道繋がり）】群馬県公式サイト')"
      :btn-text="$t('Jump!')"
    />
    <static-info
      class="mb-4"
      :url="'https://stop-covid19-nagano.netlify.app/'"
      :text="$t('【近隣県（川中島でおなじみ）】長野県非公式サイト')"
      :btn-text="$t('Jump!')"
    />
    <static-info
      class="mb-4"
      :url="'https://stopcovid19-toyama.netlify.com/'"
      :text="$t('【近隣県（親知知の向こう）】富山県公認サイト')"
      :btn-text="$t('Jump!')"
    />
    <!--<v-row class="StaticCard">
    
      <StaticCard>
        {{　$t('当サイトは新型コロナウイルス感染症 (COVID-19) に関する最新情報を提供するために、東京都が開設したものを、茨城県向けに改変したものです。')　}}<br /><br />
        {{　$t('茨城県による公式情報と客観的な数値をわかりやすく伝えることで、茨城県にお住まいの方や、茨城県内に拠点を持つ企業の方、茨城県を訪れる方が、現状を把握して適切な対策を取れるようにすることを目的としています。')　}}<br><br>
        {{ $t('なお、「非公式」とあるように、') }}{{ $t('このサイトは、茨城県が管理しているものではありません。') }}{{ $t('このサイトに関するご意見やご質問などは、県ではなくAsaにお寄せください。')}}{{ $t('県はこのサイトには一切関与しておりません。') }}
        <i18n path="詳しくは、{contact}をご確認ください。">
        <nuxt-link :to="localePath('/contacts')" place="contact">{{ $t('お問い合わせ先一覧') }}</nuxt-link>
        </i18n>
      </StaticCard>
      </v-row>-->
  </div>
</template>

<i18n src="./index.i18n.json"></i18n>

<script>
import PageHeader from '@/components/PageHeader.vue'
import WhatsNew from '@/components/WhatsNew.vue'
import StaticInfo from '@/components/StaticInfo.vue'
import Data from '@/data/data.json'
import formatGraph from '@/utils/formatGraph'
// import formatTable from '@/utils/formatTable'
import News from '@/data/news.json'
import ConfirmedCasesDetailsCard from '@/components/cards/ConfirmedCasesDetailsCard.vue'
import ConfirmedCasesNumberCard from '@/components/cards/ConfirmedCasesNumberCard.vue'
import ConfirmedCasesAttributesCard from '@/components/cards/ConfirmedCasesAttributesCard.vue'
import TestedNumberCard from '@/components/cards/TestedNumberCard.vue'
import TelephoneAdvisoryReportsNumberCard from '@/components/cards/TelephoneAdvisoryReportsNumberCard.vue'
import ConsultationDeskReportsNumberCard from '@/components/cards/ConsultationDeskReportsNumberCard.vue'
import MetroCard from '@/components/cards/MetroCard.vue'
import AgencyCard from '@/components/cards/AgencyCard.vue'
import PositiveRateCard from '@/components/cards/PositiveRateCard.vue'
import PositiveRateCard2 from '@/components/cards/PositiveRateCard2.vue'

export default {
  components: {
    PageHeader,
    WhatsNew,
    StaticInfo,
    ConfirmedCasesDetailsCard,
    ConfirmedCasesNumberCard,
    ConfirmedCasesAttributesCard,
    TestedNumberCard,
    TelephoneAdvisoryReportsNumberCard,
    ConsultationDeskReportsNumberCard,
    MetroCard,
    AgencyCard,
    PositiveRateCard,
    PositiveRateCard2
  },
  data() {
    // 退院者グラフ
    const dischargesGraph = formatGraph(Data.discharges_summary.data)
    // 死亡者数
    // #MEMO: 今後使う可能性あるので一時コメントアウト
    // const fatalitiesTable = formatTable(
    //   Data.patients.data.filter(patient => patient['備考'] === '死亡')
    // )

    const data = {
      Data,
      dischargesGraph,
      headerItem: {
        icon: 'mdi-chart-timeline-variant',
        title: this.$t('都内の最新感染動向'),
        date: Data.lastUpdate
      },
      newsItems: News.newsItems
    }
    return data
  },
  head() {
    return {
      title: this.$t('都内の最新感染動向')
    }
  }
}
</script>

<style lang="scss" scoped>
.MainPage {
  .DataBlock {
    margin: 20px -8px;
    .DataCard {
      @include largerThan($medium) {
        padding: 10px;
      }
      @include lessThan($small) {
        padding: 4px 8px;
      }
    }
  }
}
</style>
