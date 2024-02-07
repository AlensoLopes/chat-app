<script setup>
import MessageComponents from '@/components/MessageComponents.vue';
import { ref } from "vue";
const message = ref('');
const messageList = ref([]);

const addMessage = () => {
  if(message.value === '') 
    return;
  messageList.value.push({
    message: message.value,
    date: new Date(),
    user: {
      name: 'Eric Porcq',
      avatarUrl: 
      'https://media.licdn.com/dms/image/C4D03AQH0TuKfHrOpfQ/profile-displayphoto-shrink_400_400/0/1607679351861?e=2147483647&v=beta&t=a2zxWJKCOT4EasStDlHtACsP2DwoH5fFWX6uudlQpe4'
    }
  });
  message.value = '';
  console.log(messageList.value);
};
</script>

<template>
  <div class='flex flex-col w-full justify-center'>
    <div v-for="(message, index) in messageList" :key="index" class="border rounded-md p-2 m-2 bg-gray-800 flex flex-col-reverse">
      <MessageComponents :message="message" />
    </div>
    <div class='flex flex-row w-full justify-center p-2 fixed bottom-4'>
      <textarea v-model="message" name='message' id='message' rows='' class="text-black rounded-md"></textarea>
      <button @click="addMessage" class="ml-2 p-2 rounded-md bg-blue-600">Send</button>
    </div>
  </div>
</template>