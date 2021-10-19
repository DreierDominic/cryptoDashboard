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
  <div class="bg-gray-600 bg-opacity-25 hover:bg-opacity-50 p-5 mb-2 rounded-md">

    <div class="grid grid-cols-2 flex items-center">
      <h1 class="text-2xl">
        {{data.name}}
      </h1>

      <h2 class="text-5xl text-right">
        $ {{data.price_usd}}

        <TrendingUpIcon class="h-10 w-10 mb-2 inline text-green-500" v-if="Math.sign(Number(data.percent_change_1h)) > 0"/>
        <TrendingDownIcon class="h-10 w-10 mb-2 inline text-red-500" v-if="Math.sign(Number(data.percent_change_1h)) < 0"/>
      </h2>
    </div>
  </div>
</template>

<style scoped>
</style>
