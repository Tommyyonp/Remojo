<template>
  <div class="max-w-screen-sm mx-auto px-4 py-10">
    <!-- Error Handling-->
    <div v-if="errorMsg" class="mb-10  p-4 rounded-d bg-light-grey shadow-lg">
       <p class="text-red-500">{{errorMsg}}</p>
    </div>

    <!-- Registration -->
    <form 
      @submit.prevent="register" 
      class="p-8 flex flex-col"
    >

      <b class="text-4xl text-at-blue mb-4 text-center">Register</b>

      <div class="flex flex-col mb-2">
      <label for="email" class="mb-1 text-m text-at-blue">Email</label>
      <input type="text" 
      required 
      class="p-2 text-at-blue rounded-2xl border-2 border-at-blue focus:outline-at-dark-blue" 
      id="email"
      placeholder="Enter your email here..."
      v-model="email"
      /> 
    </div>

    <div class="flex flex-col mb-2">
      <label for="phoneNumber" class="mb-1 text-m text-at-blue">Phone Number</label>
      <input type="tel" 
      onkeypress="return (event.charCode !=8 && event.charCode ==0 || (event.charCode >= 48 && event.charCode <= 57))"
      required 
      class="p-2 text-at-blue rounded-2xl border-2 border-at-blue focus:outline-at-dark-blue" 
      id="phoneNumber"
      placeholder="Enter your phone number here..."
      v-model="phoneNumber"
      /> 
    </div>

    <div class="flex flex-col mb-2">
      <label for="password" class="mb-1 text-m text-at-blue">Password</label>
      <input type="password" 
      required 
      class="p-2 text-at-blue rounded-2xl border-2 border-at-blue focus:outline-at-dark-blue" 
      id="password"
      placeholder="Enter your password here..."
      v-model="password"
      /> 
    </div>

    <div class="flex flex-col mb-2">
      <label for="confirmPassword" class="mb-1 text-m text-at-blue">Confirm Password</label>
      <input type="password" 
      required 
      class="p-2 text-at-blue rounded-2xl border-2 border-at-blue focus:outline-at-dark-blue" 
      id="confirmPassword"
      placeholder="Enter your confirmation password here..."
      v-model="confirmPassword"
      /> 
    </div>
 
    <button type="submit" class="w-3/4 mt-6 py-2 px-6 rounded-2xl self-center text-sm
      text-white bg-at-blue border-solid
      border-2 border-transparent hover:border-at-blue hover:bg-white
      hover:text-at-blue"
    >Register</button>

      <router-link class="text-l mt-6 text-center text-at-blue" :to="{name: 'Login'}">
        Already have an account? Please <span class="text-at-dark-blue">Login</span>
      </router-link>
    </form>
  </div>
</template>

<script>
  import { ref } from "vue";
  import { supabase } from '../supabase/init'
  import { useRouter } from "vue-router";
 
export default {
  name: "register",
  setup() {
    // Create data / vars
    const router = useRouter(); 
    const email = ref(null);
    const password = ref(null);
    const confirmPassword = ref(null);
    const errorMsg = ref(null);

    // Register function
    const register = async () => {
      if (password.value == confirmPassword.value) {
        try {
          const {error } = await supabase.auth.signUp({
            email : email.value,
            password :  password.value,
          });
          if (error) throw error;
          router.push({name: "Login"});
        } catch(error) {
          errorMsg.value = error.message; 
          setTimeout(() => {
            errorMsg.value = null;
          }, 5000)
        }
        return;
      }
      errorMsg.value = "Error: Password do not match!";
      setTimeout(() => {
        errorMsg.value = null;
      }, 5000)
    };
 
    return {email, password, confirmPassword, errorMsg, register };
  },
};
</script>
