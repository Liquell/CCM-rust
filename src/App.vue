<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import Message from "./components/Message.vue";
import Header from "./components/Header.vue";
import Tabs from "./components/Tabs.vue";
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

async function copyMessageToClipboard(msg, index) {
  await clipboard.writeText(msg);
  moveMessageToTop(index);
}

function moveMessageToTop(index) {
  const message = clipboardHistory.value.splice(index, 1)[0];
  clipboardHistory.value.unshift(message);
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
  <Header />
  <Tabs />
  <div>
    <Message
      v-for="(msg, index) in clipboardHistory"
      :key="index"
      :msg="msg"
      @delete="deleteMessage(index)"
      @copy="copyMessageToClipboard(msg, index)"
    />
  </div>
</template>