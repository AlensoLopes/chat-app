<script setup>
import MessageComponents from '@/components/MessageComponents.vue';
import { ref } from "vue";
const message = ref('');
const messageList = ref([]);
const messageInput = ref(null)

const addMessage = () => {
  if(message.value === '') 
    return;
  messageList.value.push({
    id: Math.random().toString(32).slice(2),
    message: message.value,
    date: new Date(),
    user: {
      name: 'Jean-Luc Lambert',
      avatarUrl: 
      'https://media.licdn.com/dms/image/C4D03AQE30YtF8pwv-Q/profile-displayphoto-shrink_800_800/0/1605694187785?e=2147483647&v=beta&t=MRnxl_KBJ17-TcmyfPmWRNIecBPXQkl9KHB9h_goHOs'
    }
  });
  message.value = '';
  console.log(messageList.value);

  messageInput.value.focus()
};

const deleteMessage = (id) => messageList.value = messageList.value.filter(message => message.id !== id)

</script>

<template>
  <div class='flex flex-col w-full justify-center'>
    <div v-for="(message, index) in messageList" :key="index" class="border rounded-md p-2 m-2 bg-gray-800 flex flex-col-reverse">
      <MessageComponents @delete="deleteMessage" :message="message" />
    </div>
    <div class='flex flex-row w-full justify-center p-2 fixed bottom-4'>
      <textarea ref="messageInput"
      @keyup.enter.exact="addMessage"
      v-model="message" name='message' id='message' rows='1' class="text-black rounded-md w-full"></textarea>
      <button @delete="deleteMessage" @click="addMessage" class="ml-2 p-4 rounded-md bg-blue-600">Send</button>
    </div>
  </div>
</template>