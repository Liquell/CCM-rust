<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import Message from "./components/Message.vue";
import { clipboard } from "@tauri-apps/api";

const clipboardText = ref("");
const clipboardHistory = ref([]);

async function readClipboard() {
  const newText = await clipboard.readText();
  if (newText !== clipboardText.value) {
    clipboardText.value = newText;
    clipboardHistory.value.unshift(newText); // додаємо новий текст на початок масиву
    if (clipboardHistory.value.length > 50) {
      clipboardHistory.value.pop(); // видаляємо останній елемент, якщо масив містить більше 50 елементів
    }
  }
}

async function copyMessageToClipboard(msg) {
  await clipboard.writeText(msg);
}

function deleteMessage(index) {
  clipboardHistory.value.splice(index, 1);
}

let intervalId;

onMounted(() => {
  intervalId = setInterval(readClipboard, 1000);
});

onUnmounted(() => {
  clearInterval(intervalId);
});
</script>

<template>
  <div>
    <Message
      v-for="(msg, index) in clipboardHistory"
      :key="index"
      :msg="msg"
      @delete="deleteMessage(index)"
      @copy="copyMessageToClipboard(msg)"
    />
  </div>
</template>