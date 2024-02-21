<script setup>
import { useUserStore } from '@/stores/user';
import { supabase } from '@/supabase';
import { storeToRefs } from 'pinia';
import { useRouter } from 'vue-router';
import { ref } from 'vue';

const { user } = storeToRefs(useUserStore());
const { push: routerPush } = useRouter(); 
const loading = ref(false);

const logout = async () =>{
  loading.value = true;
  await supabase.auth.signOut();
  routerPush({ name: 'login' });
}
</script>

<template>
  <header class="flex flex-row items-center p-3">
    <div v-if="user" class="flex flex-row">
      <h1>Username : {{ user.username }}</h1>
    </div>
    <button :loading="loading" @click="logout" class="ml-auto p-2 outline rounded-md hover:text-blue-500 transition-all">
      <span v-if="loading">...</span>
      <span v-else>Se déconnecter</span>
    </button>
  </header>
</template>