<template>
  <div>
    <div v-if="coin_item != undefined" class="p-5 mr-5 md:mr-0 lg:px-16 2xl:px-20 lg:py-6 2xl:py-14 overflow-x-auto">
      <div class="table-auto w-fit">
        <thead class="bg-blue-600 text-slate-50">
          <tr>
            <th class="w-screen px-10 md:px-0 first:rounded-tl-lg last:rounded-tr-lg text-xs md:text-md lg:text-lg 2xl:text-3xl font-medium" v-for="item in item_headers" :key="item">
              <p class="md:py-1 lg:py-2 2xl:py-6 px-5 2xl:px-10 text-left">{{ item }}</p>
            </th>
          </tr>
        </thead>
        <tbody>
            <tr @click="showCoins(coins)" class="border even:bg-gray-100 odd:bg-white hover:bg-blue-600/30 transition-all duration-200 cursor-pointer" v-for="coins in coin_item" :key="coins.id">
                <td class="border border-r-transparent border-t-transparent px-5 2xl:px-10 flex py-2 lg:py-3 2xl:py-6 text-start text-xs lg:text-lg 2xl:text-3xl items-center"><img class="w-6 lg:w-8 2xl:w-10 mr-2 lg:mr-3 2xl:mr-4" :src="coins.image" alt="Logo"><p>{{ symbolName(coins.symbol) }}</p></td>
                <td class="border border-x-transparent border-t-transparent px-5 2xl:px-10 text-xs lg:text-lg 2xl:text-3xl">{{ formatter.format(coins.current_price) }}</td>
                <td class="border border-x-transparent border-t-transparent px-5 2xl:px-10 text-xs lg:text-lg 2xl:text-3xl"><span :style="formatPercent(coins.market_cap_change_percentage_24h)[0] == '-' ? 'color: red;' : 'color: green;'">{{ formatPercent(coins.market_cap_change_percentage_24h) }}</span></td>
                <td class="border border-l-transparent border-t-transparent px-5 2xl:px-10 text-xs lg:text-lg 2xl:text-3xl">{{ formatter.format(coins.market_cap) }}</td>
            </tr>
        </tbody>
        <div class="border rounded-bl-lg rounded-br-lg border-t-transparent">
          <ul class="flex justify-end px-5 py-4 lg:py-5 2xl:py-6 text-xs">
          </ul>
        </div>
      </div>
    </div>
    <div v-else class="p-5 md:mr-0 lg:px-16 2xl:px-20 lg:py-6 2xl:py-14">
      <div class="flex flex-wrap justify-center items-center gap-5 lg:gap-10">
        <div v-for="photo in photos" :key="photo">
          <img class="w-24 lg:w-44 2xl:w-96" :src="photo" alt="photo">
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, ref } from 'vue'
import router from '../../router'

defineProps(['item_headers', 'coin_item']);

const photos = ref([
  'https://assets.coingecko.com/coins/images/1/large/bitcoin.png?1696501400',
  'https://assets.coingecko.com/coins/images/279/large/ethereum.png?1696501628',
  'https://assets.coingecko.com/coins/images/325/large/Tether.png?1696501661',
  'https://assets.coingecko.com/coins/images/825/large/bnb-icon2_2x.png?1696501970'
]);

const symbolName = (name) => {
	return name.toUpperCase();
}

const formatter = new Intl.NumberFormat('en-US', {
	style: 'currency',
	currency: 'USD'
});

const formatPercent = (value) => {
  const temp = value.toString();

  if(temp[0] != '-') {
    return '+' + value.toFixed(2) + '%';
  }

  return value.toFixed(2) + '%';
};

const showCoins = (obj) => {
  router.push(`coins/${obj.id}`).catch(err => console.log(err));
}
</script>