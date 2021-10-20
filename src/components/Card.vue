<script setup>
import { TrendingUpIcon, TrendingDownIcon, MinusIcon } from '@heroicons/vue/outline';

const props = defineProps({
  data: Object,
})
</script>

<template>
    <div class="bg-gray-100 hover:bg-gray-300 p-5 mb-2 rounded-md relative cursor-pointer dark:bg-gray-500 dark:text-white dark:hover:bg-gray-600" >
      <transition name="fade" mode="out-in">
        <div v-if="data.id">
          <h1 class="text-1xl mb-4">
            {{data.name}}
          </h1>

          <h2 class="text-3xl">
            $ {{data.price_usd}}
          </h2>

          <div class="absolute top-4 right-4">
            <TrendingUpIcon class="h-6 w-6 inline text-green-500" v-if="Math.sign(Number(data.percent_change_1h)) > 0"/>
            <MinusIcon class="h-6 w-6 inline" v-if="Math.sign(Number(data.percent_change_1h)) === 0"/>
            <TrendingDownIcon class="h-6 w-6 inline text-red-500" v-if="Math.sign(Number(data.percent_change_1h)) < 0"/>
          </div>
        </div>

        <div class="animate-pulse" v-else>
          <div class="h-5 bg-gray-400 rounded w-2/4 mb-4"></div>
          <div class="h-10 bg-gray-400 w-3/4 rounded"></div>
          <div class="h-5 bg-gray-400 rounded w-5 absolute top-5 right-5"></div>
        </div>
      </transition>
    </div>
</template>

<style scoped>
</style>
