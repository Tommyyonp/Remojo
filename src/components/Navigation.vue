<template>
  <header class="bg-at-blue text-white">
    <nav class="container py-5 px-4 flex flex-col gap-4 items-center sm:flex-row">
      <div class="flex items-center gap-x-4">
        <b class="text-2xl">REMOJO</b>
      </div>
      <ul class="flex flex-1 justify-end gap-x-10">
        <router-link class="cursor-pointer" :to="{name: 'Home' }">Home</router-link>
        <router-link class="cursor-pointer" :to="{name: 'Catalogue' }">Catalogue</router-link>
        <a href="https:wa.me/08123456789">Contact Us</a>
        <router-link v-if="user" class="cursor-pointer" :to="{name: 'Create' }">Create</router-link>
        <router-link v-if="!user" class="cursor-pointer" :to="{name: 'Login'  }">Login</router-link>
        <li v-if="user " @click="logout" class="cursor-pointer">Logout</li>
      </ul>
    </nav>
  </header>
</template>

<script>
import store from '../store/index';
import {computed} from 'vue'; 
import {supabase} from '../supabase/init'
import {useRouter} from 'vue-router'; 

export default {
  setup() {
    // Get user from store
    const user = computed(() => store.state.user);


    // Setup ref to router
    const router = useRouter();

    // Logout function
    const logout = async () => {
      await supabase.auth.signOut();
      router.push({name: "Home"  });
    };

    return {logout, user};
  },
};
</script>
