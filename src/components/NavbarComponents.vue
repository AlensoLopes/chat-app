<script setup>
import { useUserStore } from '@/stores/user';
import { storeToRefs } from 'pinia';

const { user } = storeToRefs(useUserStore());
</script>

<template>
  <header class="flex flex-row items-center p-3">
    <div v-if="user" class="flex flex-row">
      <h1>Username : {{ user.username }}</h1>
    </div>
    <button class="ml-auto p-2 outline rounded-md hover:text-blue-500 transition-all">
      Se déconnecter</button>
  </header>
</template>