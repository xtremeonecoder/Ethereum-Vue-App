<!-- 
 * Ethereum Vue App
 *
 * @category   Application_Frontend
 * @package    ethereum-vue-app
 * @author     Suman Barua
 * @developer  Suman Barua <sumanbarua576@gmail.com>
 -->

<template>
  <div>
    <h1>{{ titleText }}</h1>
    <div>
      <p><strong>Price in USD:</strong> {{ priceInUsd }} USD</p>
      <p><strong>Price in BTC:</strong> {{ priceInBtc }} BTC</p>
    </div>
    <div>
      <label for="languageSelect">Select Language: </label>
      <select
        id="languageSelect"
        v-model="selectedLanguage"
        @change="changeDescriptionLanguage"
      >
        <option value="ar">Arabic</option>
        <option value="zh">Chinese</option>
        <option value="zh-tw">Chinese (Taiwan)</option>
        <option selected="selected" value="en">English</option>
        <option value="ja">Japanese</option>
        <option value="ko">Korean</option>
        <option value="ru">Russian</option>
      </select>
    </div>
    <div>
      <h3>Description:</h3>
      <p>{{ ethereumDescription }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      ethereumData: {},
      priceInUsd: 0,
      priceInBtc: 0,
      titleText: "",
      ethereumDescription: "",
      selectedLanguage: "en",
    };
  },
  mounted() {
    // Load Ethereum data on component mount
    this.fetchEthereumData();

    // Update Ethereum data every 40 seconds
    setInterval(() => {
      this.fetchEthereumData();
    }, 40000);
  },
  methods: {
    fetchEthereumData() {
      axios
        .get("https://api.coingecko.com/api/v3/coins/ethereum")
        .then((response) => {
          // Update app data
          this.ethereumData = response.data;
          this.titleText =
            this.ethereumData.localization[this.selectedLanguage];
          this.ethereumDescription =
            this.ethereumData.description[this.selectedLanguage];
          this.priceInUsd = this.ethereumData.market_data.current_price.usd;
          this.priceInBtc = this.ethereumData.market_data.current_price.btc;
        })
        .catch((error) => {
          console.error("Error fetching Ethereum data:", error);
        });
    },
    changeDescriptionLanguage() {
      // Update Ethereum description based on the selected language
      const descriptions = this.ethereumData.description;
      this.ethereumDescription =
        descriptions &&
        (descriptions[this.selectedLanguage] || descriptions.en);

      // Update title text based on selected language
      this.titleText = this.ethereumData.localization[this.selectedLanguage];
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
}
</style>
