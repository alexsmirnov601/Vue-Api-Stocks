<script>
import axios from 'axios'

export default {
  name: 'Stocks',
  data() {
    return {
      stocks: [],
      errors: [],
      selected: '',
      isLoading: true,
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
      .finally(() => {
        this.isLoading = false
      })
  },
}
</script>
<template>
  <div class="loader" v-if="isLoading">Loading...</div>
  <div v-else>
    <div class="stock">
      <div class="stock-item" v-for="stock in stocks" :key="stock.stock">
        <div class="stock-item__info">
          <div class="stock-item__cover">
            <img
              class="stock__image"
              :src="stock.image"
              :alt="stock.companyName"
            />
          </div>
          <h3 class="stock-item__title">
            {{ stock.companyName }}
            <span>{{ stock.symbol }}</span>
          </h3>
          <span class="stock-item__price">{{ stock.price }} $</span>
        </div>
      </div>
    </div>
    <h3>Get info about company</h3>
    <select class="select" v-model="selected">
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
  </div>
</template>

<style scoped></style>
