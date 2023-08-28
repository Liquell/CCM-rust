<template>
  <div class="message-wrapper" @click="$emit('copy')">
    {{ msg }}
    <button @click.stop="$emit('delete')">DEL</button>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  msg: {
    type: String,
    required: true,
  },
});
</script>

<style lang="scss" scoped>
.message-wrapper {
  margin-top: 20px;
  justify-content: space-between;
  background-color: #eee;
  padding: 1rem;
  border-radius: 0.5rem;
  display: flex;
  align-items: center;
  gap: 40px;
}
</style>