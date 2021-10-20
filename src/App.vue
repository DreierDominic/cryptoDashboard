<script setup>
import { reactive, onMounted } from 'vue';
import Card from './components/Card.vue';
import { RefreshIcon } from '@heroicons/vue/outline';

let cryptos = reactive([[]]);
let cryptosLimit = 20;

function loadData() {
  fetch(`https://api.coinlore.net/api/tickers/?limit=${cryptosLimit}`)
    .then(res => {
        return res.json();
      })
      .then(apiData => {
        cryptos[0] = apiData.data;
      })
    .catch(error => console.log(error));
};

function createSkeletonLoader() {
  for (let i = 1; i <= cryptosLimit; i++) {
    cryptos[0].push({});
  }
}

onMounted(() => {
  createSkeletonLoader();
  loadData();
});
</script>

<template>
  <div class="dark:bg-gray-700 dark:text-white">
    <div class="bg-blue-200 text-blue-700 mb-10 px-5 md:px-0 dark:bg-blue-900 dark:text-blue-300">
      <div class="container mx-auto py-20">
        <h1 class="text-5xl mb-5">
          CryptoDashboard
        </h1>

        <p class="lg:max-w-screen-md">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </p>
      </div>
    </div>

    <div class="container mx-auto px-5 md:px-0 py-10">

      <div class="grid grid-cols-1">
        <RefreshIcon class="h-8 w-8 cursor-pointer mb-10 justify-self-center" @click="loadData()" />
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
        <Card :data="crypto" v-for="crypto in cryptos[0]"/>
      </div>
    </div>
  </div>
</template>

<style>
</style>
