<script>
import { TrendingUpIcon, TrendingDownIcon } from '@heroicons/vue/outline';

export default {
  components: {
    TrendingUpIcon,
    TrendingDownIcon,
  },

  props: {
    data: {
      type: [Object],
      required: true,
    },
  },
};
</script>

<template>
  <div class="bg-gray-100 hover:bg-gray-300 p-5 mb-2 rounded-md relative cursor-pointer">
    <h1 class="text-1xl mb-4">
      {{data.name}}
    </h1>

    <h2 class="text-3xl">
      $ {{data.price_usd}}
    </h2>

    <div class="absolute top-4 right-4">
      <TrendingUpIcon class="h-6 w-6 inline text-green-500" v-if="Math.sign(Number(data.percent_change_1h)) > 0"/>
      <TrendingDownIcon class="h-6 w-6 inline text-red-500" v-if="Math.sign(Number(data.percent_change_1h)) < 0"/>
    </div>
  </div>
</template>

<style scoped>
</style>
