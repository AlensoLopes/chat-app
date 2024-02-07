<script setup>
import { computed } from 'vue';
import { TrashIcon } from '@heroicons/vue/24/solid';
const props = defineProps({
  message: {
    type: Object,
    required: true
  }
});

const emit = defineEmits(["delete"])

const formatDate = (date) => {
  const formattedDate = date.toLocaleDateString();
  const formattedTime = date.toLocaleTimeString('default', '2-digit', '2-digit');
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
  <div class="flex flex-row items-center w-full group">
    <div class='flex justify-start items-center w-full'>
      <img :src='message.user.avatarUrl' :alt='message.user.name' class="h-16 rounded-full">
      <div class='flex flex-col p-2'>
        <h2 class="text-lg">{{ message.user.name }}</h2>
        <p class="text-xs text-gray-500">{{ formattedDate }}</p>
      </div>
      <div class='flex justify-start p-4 gap-4 w-full'>
        <p class="text-lg p-2 w-full">{{ message.message }}</p>
      </div>
    </div>
    <div class='flex justify-end w-full p-4 gap-4'>
      <button @click="emit('delete', message.id)" class="group-focus group-hover:block p-2 hidden"><TrashIcon class="h-6 w-6"/></button>
    </div>
  </div>
</template>