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
      fetch('https://api.coinlore.net/api/tickers/?limit=10')
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
  <div class="container mx-auto py-10">
    <h1 class="text-5xl mb-5">
      CryptoDashboard
    </h1>

    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    </p>
  </div>

  <div class="bg-white py-20 h-screen rounded-t-3xl shadow-2xl">
    <div class="container mx-auto">
      <Card :data="crypto" v-for="crypto in cryptos[0]"/>
    </div>
  </div>

</template>

<style>
body {
  background-color: #87F6FF;
}
</style>
