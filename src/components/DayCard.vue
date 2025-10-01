<script setup>
import { computed } from 'vue';
import IconSun from '../icons/weather/IconSun.vue';
import IconCloudy from '../icons/weather/IconCloudy.vue';
import IconRainy from '../icons/weather/IconRainy.vue';

const { weatherCode, temp, date, isActive } = defineProps({
  weatherCode: Number,
  temp: Number,
  date: String,
  isActive: Boolean,
})

const iconColor = computed(() => {
  return isActive ? 'var(--color-primary-inverted)' : 'var(--color-primary)';
})
</script>

<template>
  <button class="day-card" :class="{ active: isActive }">
    <IconSun v-if="weatherCode <= 1003" :color="iconColor" />
    <IconRainy v-else-if="weatherCode >= 1006 && weatherCode < 1063" :color="iconColor" />
    <IconCloudy v-else-if="weatherCode > 1063" :color="iconColor"/>
    <div class="day-card__day">{{ date.toLocaleDateString("ru-RU", { weekday: "short" }) }}</div>
    <div class="day-card__temp">{{ temp }} °C</div>
  </button>
</template>

<style scoped>
.day-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
  padding: 20px 24px;
  border: none;
  color: var(--color-primary);
  background-color: var(--color-bg-card);
  border-radius: 10px;
  box-shadow: 1px 2px 4px 0px var(--color-bg-main);
  cursor: pointer;
}

.day-card:not(.active):hover {
  background-color: #3a434f;
}

.active {
  color: var(--color-primary-inverted);
  background-color: var(--color-primary);
}

.day-card__day {
  font-size: 20px;
}

.day-card__temp {
  font-size: 20px;
  font-weight: 700;
}

.day-card.is-active {
  background-color: var(--color-primary);
}
</style>
