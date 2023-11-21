<template>
  <div>
    <div class="p-5 mr-5 md:mr-0 lg:px-16 2xl:px-20 lg:py-6 2xl:py-14 overflow-x-auto">
      <div class="table-auto w-fit">
        <thead class="bg-blue-600 text-slate-50">
          <tr>
            <th class="w-screen px-10 md:px-0 first:rounded-tl-lg last:rounded-tr-lg text-xs md:text-md lg:text-lg 2xl:text-3xl font-medium" v-for="item in item_headers" :key="item">
              <p class="md:py-1 lg:py-2 2xl:py-6 px-5 2xl:px-10 text-left">{{ item }}</p>
            </th>
          </tr>
        </thead>
        <tbody>
            <tr class="border even:bg-gray-100 odd:bg-white" v-for="coins in coin_item" :key="coins.id">
                <td class="border border-r-transparent border-t-transparent px-5 2xl:px-10 flex py-2 lg:py-3 2xl:py-6 text-start text-xs lg:text-lg 2xl:text-3xl items-center"><img class="w-6 lg:w-8 2xl:w-10 mr-2 lg:mr-3 2xl:mr-4" :src="coins.image" alt="Logo"><p>{{ symbolName(coins.symbol) }}</p></td>
                <td class="border border-x-transparent border-t-transparent px-5 2xl:px-10 text-xs lg:text-lg 2xl:text-3xl">{{ formatter.format(coins.current_price) }}</td>
                <td class="border border-x-transparent border-t-transparent px-5 2xl:px-10 text-xs lg:text-lg 2xl:text-3xl">{{ formatPercent(coins.market_cap_change_percentage_24h) }}</td>
                <td class="border border-l-transparent border-t-transparent px-5 2xl:px-10 text-xs lg:text-lg 2xl:text-3xl">{{ formatter.format(coins.market_cap) }}</td>
            </tr>
        </tbody>
        <div class="border rounded-bl-lg rounded-br-lg border-t-transparent">
          <ul class="flex justify-end px-5 py-4 lg:py-5 2xl:py-6 text-xs">
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

defineProps(['item_headers', 'coin_item']);


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
</script>
