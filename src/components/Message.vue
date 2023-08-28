<template>
  <div class="message" @click="$emit('copy')">
    <span> {{ msg }} </span>
    <div class="button-wrap">
      <button @click.stop="$emit('delete')" class="delete">
        <svg
          width="16"
          height="16"
          viewBox="0 0 16 16"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M12.6667 2.66667H10.3333L9.66666 2H6.33333L5.66666 2.66667H3.33333V4H12.6667M3.99999 12.6667C3.99999 13.0203 4.14047 13.3594 4.39052 13.6095C4.64057 13.8595 4.97971 14 5.33333 14H10.6667C11.0203 14 11.3594 13.8595 11.6095 13.6095C11.8595 13.3594 12 13.0203 12 12.6667V4.66667H3.99999V12.6667Z"
            fill="#848584"
          />
        </svg>
      </button>
      <button class="favorite">
        <svg
          width="16"
          height="16"
          viewBox="0 0 16 16"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M8 11.5133L10.7667 13.1867C11.2733 13.4933 11.8933 13.04 11.76 12.4667L11.0267 9.32L13.4733 7.2C13.92 6.81334 13.68 6.08 13.0933 6.03334L9.87334 5.76L8.61334 2.78667C8.38667 2.24667 7.61334 2.24667 7.38667 2.78667L6.12667 5.75334L2.90667 6.02667C2.32 6.07334 2.08 6.80667 2.52667 7.19334L4.97334 9.31333L4.24 12.46C4.10667 13.0333 4.72667 13.4867 5.23334 13.18L8 11.5133Z"
            fill="#848584"
          />
        </svg>
      </button>
    </div>
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
.message {
  margin-top: 9px;
  border-radius: 9px;
  background: #fafcfc;
  padding: 9px 15px;
  overflow: hidden;
  display: flex;
  border: 1px solid #d6d6d6;
  transition: border 0.3s ease-in-out;

  &:hover {
    border: 1px solid #848584;
  }

  & > span {
    width: 320px;
    flex: 1;
    overflow: hidden;
    max-height: 90px;
    text-overflow: ellipsis;
  }
}

.button-wrap {
  width: 20px;
}

.delete {
  cursor: pointer;
  transition: scale 0.3s ease-in-out;
  &:hover {
    scale: 1.1;
  }
}

.favorite {
  cursor: pointer;
  transition: scale 0.3s ease-in-out;
  &:hover {
    scale: 1.1;
  }
}
</style>