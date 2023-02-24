<script>
import axios from 'axios'

export default {
  name: 'Stocks',
  data() {
    return {
      stocks: [],
      errors: [],
      selected: '',
    }
  },
  created() {
    axios
      .get(
        'https://financialmodelingprep.com/api/v3/profile/AAPL,MSFT,TSLA,MDB,META,V,ZM,TRIP,EA,AMZN,INTC,TSM,BABA,CSCO,CRM,ADBE,SAP,IBM,PYPL,ABNB,UBER,MU,DELL,BIDU,NOK,OZON,PINS,DIS?apikey=a1ce470e6726aefe658181cbbe48c756'
      )
      .then((res) => {
        this.stocks = res.data
      })
      .catch((e) => this.errors.push(e))
  },
}
</script>

<template>
  <div class="stock">
    <div class="stock-item" v-for="stock in stocks" :key="stock.stock">
      <div class="stock-item__info">
        <div class="stock-item__cover">
          <img :src="stock.image" :alt="stock.companyName" />
        </div>
        <h3 class="stock-item__title">
          {{ stock.companyName }}
          <span>{{ stock.symbol }}</span>
        </h3>
      </div>
      <span class="stock-item__price">{{ stock.price }} $</span>
    </div>
  </div>
  <h3>Get info about company</h3>
  <select v-model="selected">
    <option disabled value="">Select Company</option>
    <option
      v-for="stock in stocks"
      :key="stock.stock"
      :value="stock.description"
    >
      {{ stock.companyName }}
    </option>
  </select>
  <div class="info">
    {{ selected }}
  </div>
</template>

<style scoped></style>
