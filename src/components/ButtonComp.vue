<script setup></script>

<template>
  <button class="button">
    <slot>Кнопка</slot>
  </button>
</template>

<style scoped>
.button {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 53px;
  padding: 14px;
  gap: 9px;
  font-family: var(--font-family);
  font-size: 20px;
  font-weight: 600;
  color: var(--color-primary);
  background: var(--gradient);
  border: none;
  border-radius: 10px;
  cursor: pointer;
}

.button:hover {
  background: var(--gradient-inverted);
}
</style>
