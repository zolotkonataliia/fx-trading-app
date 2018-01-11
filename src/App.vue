<template>
  <div id="app">
    <template v-if="currencyExchangeRates.length">
      <rate-panel v-for="(rate, i) in currencyExchangeRates" :rate="rate" :key="rate.id"
        :class="{ 
          'increased': currencyExchangeRates[i].buy > oldCurrencyExchangeRates[i].buy,
          'decreased': currencyExchangeRates[i].buy < oldCurrencyExchangeRates[i].buy 
        }"></rate-panel>
    </template>
  </div>
</template>

<script>
import RatePanel from "./components/RatePanel.vue"
import _ from 'lodash'

let nextRateId = 1

export default {
  name: "app",
  components: {
    RatePanel
  },
  created() {
    this.oldCurrencyExchangeRates = _.cloneDeep(this.currencyExchangeRates)
  },
  mounted() {
    setInterval(() => {
      this.changeRate()
    }, 1000)
  },
  data() {
    return {
      oldCurrencyExchangeRates: [],
      currencyExchangeRates: [
        { id: nextRateId++, pair: "USD CHF", buy: 0.99143, sell: 0.99043 },
        { id: nextRateId++, pair: "GBP USD", buy: 1.28495, sell: 1.2836 },
        { id: nextRateId++, pair: "GBP CHF", buy: 1.27378, sell: 1.27147 },
        { id: nextRateId++, pair: "EUR SEK", buy: 9.632, sell: 9.6055 },
        { id: nextRateId++, pair: "USD JPY", buy: 110.467, sell: 110.417 },
        { id: nextRateId++, pair: "EUR JPY", buy: 120.589, sell: 120.491 }
      ]
    }
  },
  methods: {
    changeRate () {
      if (this.currencyExchangeRates.length) {
        this.oldCurrencyExchangeRates = _.cloneDeep(this.currencyExchangeRates)
        
        for (let i in this.currencyExchangeRates) {
          let rate = this.randomNumber()
          
          let item = this.currencyExchangeRates[i]
          let prevBuyVal = item.buy

          let buyRateNew = item.buy + item.buy * rate
          let sellRateNew = item.sell + item.buy * rate
          
          item.buy = Number(buyRateNew.toPrecision(6))
          item.sell = Number(sellRateNew.toPrecision(6))
        }
      }
    },
    randomNumber() {
      return Math.random() * 0.2 - 0.1
    }
  }
};
</script>

<style lang="scss">
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}
body {
  margin: 0;
  padding: 0;
  font: 14px "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #41403f;
  background-color: #efefef;
}
#app {
  padding: 20px;
  display: -webkit-box;
  display: -moz-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  -webkit-box-direction: normal;
  -moz-box-direction: normal;
  -webkit-box-orient: vertical;
  -moz-box-orient: vertical;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-flex-wrap: wrap;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
  -webkit-box-pack: center;
  -moz-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-align-content: center;
  -ms-flex-line-pack: center;
  align-content: center;
  -webkit-box-align: center;
  -moz-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  @media screen and (min-width: 768px) {
    padding: 50px;
    -webkit-box-orient: horizontal;
    -moz-box-orient: horizontal;
    -webkit-flex-direction: row;
    -ms-flex-direction: row;
    flex-direction: row;
    height: 100vh;
  }
}
</style>
