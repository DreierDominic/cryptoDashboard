<script>
import { reactive, onMounted } from 'vue';
import Card from './components/Card.vue';

export default {
  components: {
    Card,
  },
  setup() {
    let cryptos = reactive([]);

    function loadData() {
      fetch('https://api.coinlore.net/api/tickers/?limit=20')
        .then(res => {
            return res.json();
          })
          .then(apiData => {
            cryptos.push(apiData.data);
          })
        .catch(error => console.log(error));
    };

    onMounted(() => {
      loadData();
    });

    return {
      cryptos,
      loadData,
    };
  },
};
</script>

<template>
  <div class="bg-blue-200 text-blue-700 mb-10 px-5 md:px-0">
    <div class="container mx-auto py-20">
      <h1 class="text-5xl mb-5">
        CryptoDashboard
      </h1>

      <p class="lg:max-w-screen-md">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
      </p>
    </div>
  </div>

  <div class="container mx-auto px-5 md:px-0 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
    <Card :data="crypto" v-for="crypto in cryptos[0]"/>
  </div>

</template>

<style>
</style>
