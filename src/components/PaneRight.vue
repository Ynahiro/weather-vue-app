<script setup>
import { computed } from 'vue';
import { errorMap } from '../constants';

import SelectCityComp from './SelectCityComp.vue';
import StatComp from './StatComp.vue';
import ErrorComp from './ErrorComp.vue';
import DayCard from './DayCard.vue';

const { error, data, activeIndex } = defineProps({
  error: Object,
  data: Object,
  activeIndex: Number,
})

const emit = defineEmits(['select-index']);

const errorDisplay = computed(() => {
  return errorMap.get(error?.error?.code);
})

const statData = computed(() => {
  return [
    {
      label: 'Влажность',
      stat: data.forecast.forecastday[activeIndex].day.avghumidity + '%',
    },
    {
      label: 'Вероятность дождя',
      stat: data.forecast.forecastday[activeIndex].day.daily_chance_of_rain + '%',
    },
    {
      label: 'Ветер',
      stat: data.forecast.forecastday[activeIndex].day.maxwind_kph + ' км/ч',
    },
  ];
});
</script>

<template>
  <ErrorComp v-if="error" :error="errorDisplay" />
  <div v-if="data" class="stat-list">
    <div class="stat-data">
      <StatComp v-for="item in statData" :key="item.label" v-bind="item" />
    </div>

    <div class="day-cards">
      <DayCard
v-for="(item, index) in data.forecast.forecastday" :key="item.date"
        :weather-code="item.day.condition.code" :temp="item.day.avgtemp_c" :date="new Date(item.date)"
        :is-active="activeIndex == index" @click="() => emit('select-index', index)" />
    </div>
  </div>
  <SelectCityComp />
</template>

<style scoped>
.day-cards {
  display: flex;
  column-gap: 1px;
}

.stat-list {
  display: grid;
  margin-bottom: 70px;
  row-gap: 80px;
}

.stat-data {
  display: grid;
  row-gap: 16px;
}
</style>
