<script setup>
  import { supabase } from '@/supabase'
  import { useUserStore } from './stores/user';
  
  supabase.auth.onAuthStateChange((_, session) => {
    useUserStore().fetchUserProfile(session?.user?.id);
  })

</script>

<template>
  <div class='bg-gray-800 text-white min-h-[100vh] flex flex-col'>
    <RouterView />
  </div>
</template>