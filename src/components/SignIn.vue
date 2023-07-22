<!-- COMPONENTE BOILERPLATE -->

<template>
  <div>
  
    <div>
      <h1>Task Planner</h1>
      <img src="/assets/Task Planner.png" alt="Logo">
    </div>

    <div v-show="errorMsg" class="error"> {{ errorMsg }}</div>
  
    <div class="container">
      
      <form @submit.prevent="login">
        <h2>Login</h2>
        
        <div class="input">
          <label for="email">Email address</label>
          <input
            class="form-control"
            type="email"
            placeholder="email@adress.com"
            v-model="email"
            required
          />
        </div>
        
        <div class="input">
          <label for="password">Password</label>
          <input
            class="form-control"
            :type="passwordVisible ? 'text' : 'password'"
            placeholder="password123"
            v-model="password"
            required
          />
          <span class="toggle-password" @click="togglePasswordVisibility('password')">
            <i class="fa" :class="passwordVisible ? 'fa-eye-slash' : 'fa-eye'"></i>
          </span>   
        </div>
        
        <button type="submit" class="btn-pers" id="login_button">
          Login
        </button>
        
        <p>You don't have an account? <PersonalRouter :route="route" :buttonText="buttonText" class="sign-up-link"/></p>

      </form>
    
    </div>
  </div>
</template>

<script>
import PersonalRouter from "./PersonalRouter.vue";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { ref } from 'vue';

const route = "/auth/signup";
const buttonText = "Sign Up";

const email = ref("");
const password = ref("");
const redirect = useRouter();
const userStore = useUserStore();

// Error Message if incorrect data is entered 
const errorMsg = ref("");

const signIn = async () => {
  try {
    await userStore.signIn(email.value, password.value);
    redirect.push("/");
  } catch (error) {
    console.error(error);
    errorMsg.value = "Incorrect email or password.";
    setTimeout(() => {
      errorMsg.value = null;
    }, 3000);
  }
    return;
  }


//V Visibility and confirmation of password
const passwordVisible = ref(false);
const confirmPasswordVisible = ref(false);

const togglePasswordVisibility = (field) => {
  if (field === "password") {
    passwordVisible.value = !passwordVisible.value;
  } else if (field === "confirmPassword") {
    confirmPasswordVisible.value = !confirmPasswordVisible.value;
  }
};

</script>

<style scoped>
.container {
  width: 400px;
  max-width: 95%;
}

.input {
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

.input > label {
  text-align: start;
}

.input > input {
  margin-top: 6px;
  height: 38px !important;
}

.btn-pers {
  position: relative;
  left: 50%;
  padding: 1em 2.5em;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 2.5px;
  font-weight: 700;
  color: #000;
  background-color: #fff;
  border: none;
  border-radius: 45px;
  box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease 0s;
  cursor: pointer;
  outline: none;
  transform: translateX(-50%);
}

.btn-pers:hover {
  background-color: #198754;
  box-shadow: 0px 15px 20px rgba(46, 229, 157, 0.4);
  color: #fff;
  transform: translate(-50%, -7px);
}

.btn-pers:active {
  transform: translate(-50%, -1px);
}

.register {
  text-align: center;
}

.register > span {
  color: #0d6efd;
  cursor: pointer;
}

</style>
