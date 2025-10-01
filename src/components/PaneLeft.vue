<script setup>
import { computed, inject } from 'vue';
import { cityProvide } from '../constants';

import IconSun from '../icons/weather/IconSun.vue';
import IconCloudy from '../icons/weather/IconCloudy.vue';
import IconRainy from '../icons/weather/IconRainy.vue';
import IconLocation from '../icons/IconLocation.vue';

const { dayData } = defineProps({
  dayData: Object,
})

const city = inject(cityProvide);

const weekDay = computed(() => {
  return new Date(dayData.date).toLocaleDateString('ru-Ru', { weekday: 'long' });
})

const fullDate = computed(() => {
  return new Date(dayData.date).toLocaleDateString('ru-Ru', { year: 'numeric', month: 'long', day: 'numeric' });
})

const weatherCode = computed(() => {
  return dayData.day.condition.code;
})

</script>

<template>
  <div class="paneLeft">
    <div class="day-info">
      <div class="day">{{ weekDay }}</div>
      <div class="date">{{ fullDate }}</div>
      <div class="city">
        <IconLocation />
        {{ city }}
      </div>
    </div>
    <div class="weather-info">
      <div class="weatherIcon">
        <IconSun v-if="weatherCode <= 1003" />
        <IconRainy v-else-if="weatherCode >= 1006 && weatherCode < 1063" />
        <IconCloudy v-else-if="weatherCode > 1063" />
      </div>
      <div>
        <div class="temp">{{ dayData.day.avgtemp_c }} °C</div>
        <div class="condition">{{ dayData.day.condition.text }}</div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.paneLeft {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
  padding: 48px 32px;
}

.day {
  font-size: 37px;
  font-weight: 700;
  margin-bottom: 16px;
  text-transform: capitalize;
}

.date {
  font-size: 22px;
  font-weight: 500;
  margin-bottom: 10px;
}

.weatherIcon {
  margin-bottom: 25px;
}

.city {
  display: flex;
  align-items: center;
  gap: 8px;
}

.temp {
  font-size: 50px;
  font-weight: 700;
  margin-bottom: 9px;
}

.condition {
  font-size: 30px;
  font-weight: 700;
}
</style>
