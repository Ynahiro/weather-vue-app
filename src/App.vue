<script setup lang="js">
import { onMounted, provide, ref, watch } from 'vue';
import { API_ENDPOINT, cityProvide } from './constants';

import PaneRight from './components/PaneRight.vue';
import PaneLeft from './components/PaneLeft.vue';

const data = ref();
const error = ref('');
const activeIndex = ref(0);
const city = ref('Moscow');

provide(cityProvide, city);

watch(city, () => {
  getCity(city.value);
})

onMounted(() => {
  getCity(city.value);
})

function selectIndex(index) {
  activeIndex.value = index;
}

async function getCity(city) {
  const params = new URLSearchParams({
    q: city,
    lang: 'ru',
    key: '798dd70229d848f9930140623252609',
    days: 3
  });

  const res = await fetch(`${API_ENDPOINT}/forecast.json?${params}`)
  if (res.status !== 200) {
    error.value = await res.json();
    data.value = null;
    return;
  } else {
    error.value = null;
    data.value = await res.json(); }
}

</script>

<template>
  <main class="main">
    <div class="left">
      <PaneLeft v-if="data" :day-data="data.forecast.forecastday[activeIndex]" />
    </div>
    <div class="right">
      <PaneRight :error :data :active-index="activeIndex" @select-index="selectIndex" @select-city="getCity" />
    </div>
  </main>
</template>

<style scoped>
.main {
  display: flex;
  align-items: center;
  justify-content: center;
}

.left {
  width: 500px;
  height: 720px;
  background: url('../public/bg.png') center/cover no-repeat;
  border-radius: 30px;
}

.right {
  padding: 60px 50px;
  background-color: var(--color-bg-main);
  border-radius: 0px 25px 25px 0px;
}
</style>
