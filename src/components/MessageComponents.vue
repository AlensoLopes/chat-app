<script setup>
import { computed } from 'vue';
const props = defineProps({
  message: {
    type: Object,
    required: true
  }
});

const formatDate = (date) => {
  let formattedDate = date.toLocaleDateString();
  let formattedTime = date.toLocaleTimeString('default', '2-digit', '2-digit');
  if(formattedDate === new Date().toLocaleDateString())
    return `Aujourd'hui à ${formattedTime}`;
  return `${formattedDate} à ${formattedTime}`;
};

const formattedDate = computed(() => {
  const date = new Date(props.message.date);
  return formatDate(date);
});
</script>

<template>
  <div class="flex flex-row items-center w-full">
    <div class='flex justify-start items-center'>
      <img :src='message.user.avatarUrl' :alt='message.user.name' class="h-16 rounded-full">
      <div class='flex flex-col p-2'>
        <h2 class="text-lg">{{ message.user.name }}</h2>
        <p class="text-xs text-gray-500">{{ formattedDate }}</p>
      </div>
    </div>
    <div class='flex justify-center p-4'>
      <p class="text-lg p-2">{{ message.message }}</p>
    </div>
  </div>
</template>