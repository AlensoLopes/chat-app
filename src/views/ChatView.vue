<script setup>
import MessageComponents from '@/components/MessageComponents.vue';
import NavbarComponents from '@/components/NavbarComponents.vue';
import { ref, onMounted } from "vue";
import { useUserStore } from '@/stores/user';
import { storeToRefs } from 'pinia';
import { insertMessage, fetchMessage, subscribeToMessages, messageList } from '@/api/messages';

const message = ref('');
const messageInput = ref(null);

subscribeToMessages();

onMounted(async () =>  await fetchMessage());

const { user } = storeToRefs(useUserStore());

const addMessage = async () => {
  if(message.value === '') 
    return;

  await insertMessage(message.value, user.value.id);
  message.value = '';
  messageInput.value.focus()
};


const deleteMessage = (id) => messageList.value = messageList.value.filter(message => message.id !== id)

</script>

<template>
  <div class='flex flex-col w-full justify-center overflow-hidden'>
    <NavbarComponents/>
  <div class='overflow-auto grow'>
    <div v-for="(message, index) in messageList" :key="index" class="border rounded-md p-2 m-2 bg-gray-800 flex flex-col-reverse">
      <MessageComponents @delete="deleteMessage" :message="message" />
    </div>
    <div class='flex flex-row w-full justify-center p-2 fixed bottom-4'>
      <textarea ref="messageInput"
      @keyup.enter.exact="addMessage"
      v-model="message" name='message' id='message' rows='1' class="text-black rounded-md"></textarea>
      <button @delete="deleteMessage" @click="addMessage" class="ml-2 p-4 rounded-md bg-blue-600">Send</button>
    </div>
  </div>
  </div>
</template>