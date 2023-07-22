<!-- COMPONENTE BOILERPLATE -->
 
<template>

  <div class="container">
    <h3 class="header-title">Task Planner</h3>
    <img src="/assets/Task Planner.png" alt="Logo">
    <p class="header-subtitle">Your Ultimate Task Management App!</p>

    <div>
        <form @submit.prevent="signIn" class="form-sign-in">
        <div class="form">
          <div class="form-input">
            <label class="input-field-label">E-mail</label>
            <input
              type="email"
              class="input-field"
              placeholder="example@gmail.com"
              id="email"
              v-model="email"
              required
            />
          </div>
          <div class="form-input">
            <label class="input-field-label">Password</label>
            <div class="password-input">
            <input
              type="text"
              class="input-field"
              placeholder="**********"
              v-model="password"
              required
            />
            </div>
          </div>
            <button class="button" type="submit">Login</button>
        </div>
      </form>
      <div v-show="errorMsg">{{errorMsg}}</div>
    </div>

    <p>You don't have an account? <PersonalRouter :route="route" :buttonText="buttonText" class="sign-up-link"/></p>
  </div>

</template>

<script setup>
import PersonalRouter from "./PersonalRouter.vue";
import { ref, reactive } from "vue";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";


// Route Variables
const route = "/auth/signup";
const buttonText = "Sign Up";

// Input Fields
const email = ref("");
const password = ref("");

// Error Message
const errorMsg = ref("");

// Router to push user once SignedIn to the homeView
const redirect = useRouter();

// Arrow function to Signin user to supaBase
const signIn = async () => {
  try {
    await useUserStore().signIn(email.value, password.value);
    // redirects user to the homeView
    redirect.push({ path: "/" });
  } catch (error) {
    alert(error);
  }
};


</script>

<style>

</style>