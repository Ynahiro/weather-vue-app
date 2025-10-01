<script setup>
const data = defineModel({ type: String, required: true });
</script>

<template>
  <input v-model="data" class="input" name="city" type="text" />
</template>

<style scoped>
.input {
  width: 260px;
  height: 53px;
  padding: 15px 20px;
  font-size: 18px;
  color: var(--color-primary);
  border: none;
  background-color: var(--color-bg-card);
  border-radius: 10px;
  box-shadow: 1px 2px 4px 0px var(--color-bg-main);
}

.input::placeholder {
  color: var(--color-text-placeholder);
}
</style>
