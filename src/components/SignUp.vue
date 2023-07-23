<template>
  
  <div class="box-form">
<!-- Left side of box form -->
    <div class="left">
        <div class="overlay">
          <img src="/assets/TaskMaster.png" alt="Logo">
          <h1>Task Master</h1>
          <p>Your Ultimate Task Management App!</p>
      </div>
    </div>
<!-- Right side of box form -->
    <div class="right">
      <form @submit.prevent="signUp">
        <div class="form">
          <h3>REGISTER</h3>
          <div class="inputs">
            <label>E-mail</label><br>
            <input
              type="email"
              class="input-field"
              placeholder="example@gmail.com"
              id="email"
              v-model="email"
              required
            />
          </div>
          <div class="inputs">
            <label>Password</label>
            <input
              type="password"
              class="input-field"
              placeholder="**********"
              id="password"
              v-model="password"
              required
            />
          </div>
          <div class="inputs">
            <label>Confirm password</label>
            <input
              type="password"
              class="input-field"
              placeholder="**********"
              id="confirmPassword"
              v-model="confirmPassword"
              required
            />
          </div>
          <button class="button" type="submit">Sign Up</button>
          </div>    
      </form>
      <p> Have an account? <PersonalRouter :route="route" :buttonText="buttonText"/>
      </p>
    </div>
  </div>
    <div v-show="errorMsg">{{errorMsg}}</div>
</template>

<script setup>
import { ref, computed } from "vue";
import PersonalRouter from "./PersonalRouter.vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";

// Route Variables
const route = "/auth/login";
const buttonText = "Login";

// Input Fields
const email = ref("");
const password = ref("");
const confirmPassword = ref("");

// Error Message
const errorMsg = ref("");

// Router to push user once SignedUp to Log In
const redirect = useRouter();

// Arrow function to SignUp user to supaBase with a timeOut() method for showing the error
const signUp = async () => {
  if (password.value === confirmPassword.value) {
    try {
      // calls the user store and send the users info to backend to logIn
      await useUserStore().signUp(email.value, password.value);
      // redirects user to the homeView
      redirect.push({ path: "/auth/login" });
    } catch (error) {
      // displays error message
      errorMsg.value = error.message;
      // hides error message
      setTimeout(() => {
        errorMsg.value = null;
      }, 5000);
    }
    return;
  }
  errorMsg.value = "Incorrect email or password. Please try again.";
};
</script>

<style></style>
