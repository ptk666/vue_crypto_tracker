<template>
  <div class="home w-screen h-screen bg-blue-600 text-white overflow-hidden">
    <Navbar />
    <Front />
  </div>
  <MarketMessage />
  <TableCrypto 
    :item_headers="item_headers"
    :coin_item="coin_item"
  />
  <div class="p-5 lg:px-16 2xl:px-20 lg:py-6 2xl:py-14">
  </div>
  <Secure />
  <Testimonials />
  <Download />
  <div class="mt-10 bg-blue-600 text-white">
    <div class="p-1 2xl:p-2 flex justify-center">
      <p class="text-xs 2xl:text-xl">Subscribe to our newsletter!</p>
    </div>
  </div>
  <div class="p-5 lg:px-16 2xl:px-20 lg:py-6 2xl:py-14">
    <div class="grid grid-cols-2 grid-rows-1">
      <div>
        <h1 class="font-semibold text-2xl lg:text-4xl 2xl:text-6xl">Crypto</h1>
        <div class="mt-2 lg:mt-4 2xl:mt-10 flex">
          <a class="border p-1 lg:p-2 rounded cursor-pointer" target="_blank" src="https://github.com/ptk666"><img class="w-5 2xl:w-10" src="/assets/images/github.png" alt=""></a>
          <a class="ml-1 lg:ml-2 border p-1 lg:p-2 rounded cursor-pointer" target="_blank" src="https://www.linkedin.com/in/brucejamesdelacruz/"><img class="w-5 2xl:w-10" src="/assets/images/linkedin.png" alt=""></a>
        </div>
      </div>
      <div>
        <p class="text-xs lg:text-sm 2xl:text-2xl text-gray-600">Product</p>
        <ul class="text-sm lg:text-base 2xl:text-3xl mt-1 md:flex md:gap-2 cursor-pointer">
          <li>Watch</li>
          <li>Features</li>
          <li>Feedback</li>
        </ul>
      </div>
    </div>
  </div>
  <div class="bg-gray-100">
    <div class="p-1">
      <p class="text-xs 2xl:text-xl text-center">Built by James</p>
    </div>
  </div>
</template>

<script setup>
/* eslint-disable */
import Navbar from '../components/HomeView/NavbarComponent.vue'
import Front from '../components/HomeView/FrontComponent.vue'
import MarketMessage from '../components/HomeView/MarketMessageComponent.vue'
import TableCrypto from '../components/HomeView/TableComponent.vue'
import Secure from '../components/HomeView/SecureComponent.vue'
import Testimonials from '../components/HomeView/TestimonialComponent.vue'
import Download from '../components/HomeView/DownloadComponent.vue'
import axios from 'axios'
import { ref, onMounted, nextTick } from 'vue'

const coin_item = ref();
const item_headers = ref(['Coin', 'Price', '24h Change', 'Market Cap']);


const getMarketCoin = async () => {
  await axios.get('https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false&locale=en')
    .then((res) => {
      const temp = [];

      for(let i = 0; i < 5; i++) {
        temp.push(res.data[i]);
      }

      coin_item.value = temp;
    })

    .catch((err) => {
      console.log(err);
      console.log(coin_item.value);
    })
}

onMounted(async () => {
  await nextTick();

  await getMarketCoin();
});
</script>

<style scoped>
  .div-table {
    width: 300vw;
  }
</style>

