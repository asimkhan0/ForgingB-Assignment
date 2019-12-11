<template>
  <div class="container">
    <h1 class="heading">Ethereum</h1>
    <select v-model="language">
      <option value="en">English</option>
      <option value="ru">Russian</option>
      <option value="ja">Japanese</option>
    </select>
    <template v-if="!ethData.market_data">
      <h2>Loading Data ...</h2>
    </template>
    <template v-else>
      <h2>Eth Val: {{ ethData.market_data.current_price.eth }}</h2>
      <h2>BitCoin: {{ ethData.market_data.current_price.btc }}</h2>
      <h2>USD : {{ ethData.market_data.current_price.usd }}</h2>

      <p class="description" v-html="ethData.description[language]" />
    </template>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "home",
  data() {
    return {
      ethData: {},
      intervalPointer: null,
      language: "en"
    };
  },
  async created() {
    this.ethData = await this.fetchEthereumData();
    this.intervalPointer = setInterval(async () => {
      this.ethData = await this.fetchEthereumData();
    }, 40000);
  },
  methods: {
    async fetchEthereumData() {
      try {
        const response = await axios.get(
          "https://api.coingecko.com/api/v3/coins/ethereum"
        );
        console.log(response);
        if (response.status === 200) {
          return response.data;
        }
      } catch (error) {
        console.log("error while requestion eth data: ", error);
      }
    }
  },
  beforeDestroy() {
    clearInterval(this.intervalPointer);
  }
};
</script>
<style scoped>
.container {
  width: 80%;
  margin: 0px auto;
}

.heading {
  background-color: grey;
}

.description {
  margin-top: 32px;
}
</style>
