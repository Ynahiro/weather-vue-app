<script setup>
import { inject, ref } from 'vue';
import { cityProvide } from '../constants';

import IconLocation from '../icons/IconLocation.vue';
import ButtonComp from './ButtonComp.vue';
import InputComp from './InputComp.vue';

const isEdited = ref(false);

const city = inject(cityProvide);
const inputValue = ref(city.value);

function editMode() {
  isEdited.value = true;
}

function save() {
  isEdited.value = false;
  city.value = inputValue.value;
}
</script>

<template>
  <div class="select-city">
    <div v-if="isEdited" class="city-input">
      <InputComp v-model="inputValue" v-focus placeholder="Введите город"  @keyup.enter="save()"/>
      <ButtonComp @click="save()"> Сохранить </ButtonComp>
    </div>
    <ButtonComp v-else @click="editMode">
      <IconLocation />
      Изменить город
    </ButtonComp>
  </div>
</template>

<style scoped>
.select-city {
  width: 420px;
}

.city-input {
  display: flex;
  gap: 12px;
}
</style>
