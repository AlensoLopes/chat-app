<script setup>
import { ref } from 'vue';
import { supabase } from '@/supabase';
import { useRouter } from 'vue-router';

const email = ref('');
const username = ref('');
const password = ref('');

const { push: routerPush } = useRouter();

const onSubmit = async () => {
  if(!email.value || !username.value || !password.value)
    return;
  const [ error ] = await supabase.auth.signUp({
    email: email.value,
    password: password.value,
    options: {
      data: { username: username.value }
    }
  });
  
  if(error) {
    console.error(error);
    return;
  }

  routerPush('/')
};

</script>

<template>
  <form class="flex flex-col gap-2 p-4 mx-auto max-w-96 w-full" @submit.prevent="onSubmit">
    <h1 class="text-2xl text-center font-bold">Créer un compte</h1>
    <div class="flex flex-col">
      <label for="email" class="font-bold">Email</label>
      <input type="email" id="email" v-model="email"
        class="p-2 bg-slate-500 rounded-md focus:bg-slate-600 transition-all" />
    </div>
    <div class="flex flex-col">
      <label for="username" class="font-bold">Username</label>
      <input type="text" id="username" v-model="username"
      class="p-2 bg-slate-500 rounded-md focus:bg-slate-600 transition-all" />
    </div>
    <div class="flex flex-col">
      <label for="password" class="font-bold">Mot de passe</label>
      <input type="password" id="password" v-model="password"
      class="p-2 bg-slate-500 rounded-md focus:bg-slate-600 transition-all" />
    </div>
    <button type="submit" class="p-2 mt-4 bg-blue-500 rounded-md
    hover:opacity-50 transition-all">Créer un compte</button>
  </form>
</template>