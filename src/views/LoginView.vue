<script setup>
import { ref } from 'vue';
import { supabase } from '@/supabase';
import { useRouter } from 'vue-router';
import AppButton from '@/components/AppButton.vue';

const email = ref('');
const password = ref('');

const { push: routerPush } = useRouter();

const onSubmit = async () => {
  if(!email.value || !password.value)
    return;
  const { error } = await supabase.auth.signInWithPassword({
    email: email.value,
    password: password.value
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
      <label for="password" class="font-bold">Mot de passe</label>
      <input type="password" id="password" v-model="password"
      class="p-2 bg-slate-500 rounded-md focus:bg-slate-600 transition-all" />
    </div>
    <AppButton>Se connecter</AppButton>
  </form>
</template>