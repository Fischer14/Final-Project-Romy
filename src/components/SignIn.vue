<!-- COMPONENTE BOILERPLATE -->
 
<template>
    <div class="box-form">
<!-- Left side of box form -->
      <div class="left">
        <div class="overlay">
            <img src="/assets/TaskMaster.png" alt="Logo">
            <h1>Task Master</h1>
            <p>Welcome back! Log in to your <br/> Ultimate Task Management App!</p>
        </div>
      </div>   
<!-- Right side of box form -->
      <div class="right">
        <form @submit.prevent="signIn">
          <div class="form">
            <h3>LOGIN</h3>
            <div class="inputs">
              <label>E-mail</label>
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
              <div class="inputs">
                <input
                  type="password"
                  class="input-field"
                  placeholder="**********"
                  id="password"
                  v-model="password"
                  required
                />
            </div>
            <div class="remember-me--forget-password">
                <input type="checkbox" checked />
                <span class="text-checkbox">Remember me</span>
            </div>
              <!-- Button access to homeView-->
              <button class="button" type="submit">Login</button>
            </div>
          </div>
        </form> 

         <!-- Link access to signUp page-->
        <p>You don't have an account? <PersonalRouter :route="route" :buttonText="buttonText"/></p>

        <div v-show="errorMsg">{{errorMsg}}</div>
      </div>
     
    </div>
</template>

<script setup>
import PersonalRouter from "./PersonalRouter.vue";
import { ref, reactive } from "vue";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";


// Route Variables
const route = "/auth/signup";
const buttonText = "Register";

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
* {
  font-family: 'Roboto', sans-serif;
  margin: 0;
}

.box-form {
  margin: 100px auto;
  width: 60%;
  background: #FFFFFF;
  border-radius: 10px;
  overflow: hidden;
  display: flex;
  flex: 1 1 100%;
  align-items: center;
  justify-content: space-evenly;
  box-shadow: 0 0 20px 6px #090b6f85;
}
@media (max-width: 980px) {
  .box-form {
    flex-flow: wrap;
    text-align: center;
    align-content: center;
    align-items: center;
  }
}

.box-form div {
  height: auto;
}

/* Left side of box form */
.box-form .left {
  color: #0f5257;
  background-size: cover;
  background-repeat: no-repeat;
  background-image: url("/assets/pexels-eberhard-grossgasteiger-2310713.jpg");
  overflow: hidden;
}
.box-form .left .overlay {
  padding: 50px;
  height: 100%;
  background: #cfd0dda1;
  overflow: hidden;
  box-sizing: border-box;
}
.box-form .left .overlay h1 {
  font-size: 7vmax;
  line-height: 1;
  font-weight: 900;
  margin-top: 30px;
  margin-bottom: 30px;
}

.box-form .left .overlay img {
  width: 18em;
  margin: -7%;
}

.box-form .left .overlay p {
  font-size: 2vmax;
  line-height: 1;
  font-weight: 200;
  margin-top: 30px;
  margin-bottom: 30px;
}

.box-form .right {
  padding: 40px;
  margin: 40px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
@media (max-width: 980px) {
  .box-form .right {
    width: 100%;
  }
}

.box-form .right .inputs {
  overflow: hidden;
}
.box-form .right h3 {
  font-size: 2vmax;
  line-height: 1;
  font-weight: 500;
  margin-top: 30px;
  margin-bottom: 30px;
}
.box-form .right label {
  font-size: 17px;
  margin: 5px;
  color: #0b3142;
  font-weight: 300;
}
.box-form .right input {
  width: 15em;
  padding: 10px;
  padding-left: 2px;
  margin-top: 10px;
  margin-bottom: 20px;
  font-size: 16px;
  border-radius: 10px;
}
.box-form .right .remember-me--forget-password {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.box-form .right .remember-me--forget-password input {
  margin: 0;
  margin-right: 7px;
  width: auto;
}


.button {
  margin: 15px;
  padding: 18px;
  margin-left: 50%;
  margin-bottom: 15%;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 2.5px;
  font-weight: 700;
  color: #fff;
  background: #0f5257;
  border: none;
  border-radius: 45px;
  box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease 0s;
  cursor: pointer;
  outline: none;
  transform: translateX(-50%);
}

.button:hover {
  background: #093c54;
  box-shadow: 0px 15px 20px #0b3142;
  transform: translate(-50%, -7px);
}

.button:active {
  transform: translate(-50%, -1px);
}

</style>