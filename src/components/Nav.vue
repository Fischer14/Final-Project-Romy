<template>
  <nav>
    <div class="navbar">
      <div class="acc-welcome">
        <router-link to="/src/views/Account.vue"><img src="/assets/avatar.jpeg" alt="avatar"></router-link>
        <p>Welcome, {{ getEmailPrefix(getUser.email) }} </p>
      </div>
      <div class="logo">
        <router-link to="/"><img alt="logo" src="/assets/TaskMasterLogo.png"></router-link>
      </div>
       <button @click="signOut" class="log-out">Log out</button> 
    </div>
  </nav>
</template>

<script setup>
// import PersonalRouter from "./PersonalRouter.vue";
import { useUserStore } from "../stores/user";
import { useRouter } from "vue-router";
import { ref, computed } from 'vue';

// constant to save a variable that will get the user from store with a computed function imported from vue
// const getUser = computed(() => useUserStore().user);
const getUser = useUserStore().user;

// constant that calls user email from the useUSerStore
const userEmail = getUser.email;

// async function that calls the signOut method from the useUserStore and pushes the user back to the Auth view.
const redirect = useRouter();

const signOut = async () => { 
  try { 
    await useUserStore().signOut();
    // call the user store and send the users info to backend to signOut
   redirect.push({ path: "/auth/login" });
    // then redirect user to the homeView
  } catch (error) {}
};

// Esta función es para mostrar solamente el prefijo del correo electrónico del usuario
const getEmailPrefix = (email) => {
  const atIndex = email.indexOf("@");
  if (atIndex !== -1) {
    return email.slice(0, atIndex);
  }
  return email;
};

</script>

<style>

nav .navbar {
  color: #0b3142;
  background-color: #c6b9cd;
  height: 150px;
  width: 100%;
  margin: 0;
  padding: 0 20px;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

@media (max-width: 980px) {
  nav .navbar {
    flex-flow: wrap;
    text-align: center;
    align-content: center;
    align-items: center;
  }
}

nav .acc-welcome {
  list-style: none;
  padding-inline-start: 5px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

nav .logo img {
  margin-top: 25px;
  width: 270px;
}


nav .acc-welcome img {
  width: 50px;
  padding: 10px;
}

.log-out {
  padding: 15px;
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

.log-out:hover {
  background: #093c54;
  box-shadow: 0px 15px 20px #0b3142;
  transform: translate(-50%, -7px);
}

.log-out:active {
  transform: translate(-50%, -1px);
}

</style>