<!-- COMPONENTE BOILERPLATE -->

<!-- User Stories -->
<!--
Feature: Log in to the app
  Background: As a user, I want to log in to the to-do app
  Given I already have an account

Scenario: As a user, I want to log in to the app
  When I visit the login page
  And I enter my email as "test@example.co.uk"
  And I enter my password as "****"
  And I click the Log In button
  Then I expect to be logged in to the app
  And I expect to see the home screen
 -->

  <template>

  <div class="container">
   <h2>Sign In</h2>
    <form @submit.prevent="signIn">
      <div>
        <label for="email">Email:</label>
        <input
          type="email"
          id="email"
          v-model.trim="email"
          :class="{ 'is-invalid': !isEmailValid }"
        />
        <div v-if="!isEmailValid" class="error-message">Invalid email</div>
      </div>
      <div>
        <label for="password">Password:</label>
        <input
          type="password"
          id="password"
          v-model.trim="password"
          :class="{ 'is-invalid': !isPasswordValid }"
        />
        <div v-if="!isPasswordValid" class="error-message">Invalid password</div>
      </div>
      <button type="submit">Sign In</button>
    </form>
    <div>
      <button @click="signInWith('Google')">Google</button>
      <button @click="signInWith('Facebook')">Facebook</button>
    </div>
    <div>
      <!-- link to sign up page -->
    </div>
  </div>

</template>

<script>
import PersonalRouter from "./PersonalRouter.vue";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { ref, computed } from 'vue';

// Route Variables
const route = "/auth/signup";
const buttonText = "Sign Up";

export default {
  setup() {
    const email = ref('');
    const password = ref('');
    const showPassword = ref(false);

    const isEmailValid = computed(() => {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return emailRegex.test(email.value);
    });

    const isPasswordValid = computed(() => {
      return password.value.length >= 6;
    });

    const signIn = () => {
      if (isEmailValid.value && isPasswordValid.value) {
        // Perform sign in logic here
        console.log('Signed In');
      }
    };

    const signInWith = (provider) => {
      // Perform sign in with social media logic here
      console.log(`Signing In with ${provider}`);
    };

    const goToSignUp = () => {
      // Redirect to Sign Up page
      console.log('Going to Sign Up');
    };

    return {
      email,
      password,
      showPassword,
      isEmailValid,
      isPasswordValid,
      signIn,
      signInWith,
      goToSignUp
    };
  }
};




// Arrow function to Signin user to supaBase
// const signIn = async () => {
//   try {

//   } catch (error) {}
// };
</script>

<style>
.is-invalid {
  border: 1px solid red;
}

.error-message {
  color: red;
}
</style>
