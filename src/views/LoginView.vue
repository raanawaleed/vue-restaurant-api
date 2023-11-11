<template>
  <div>
    <form @submit.prevent="login">
      <input v-model="email" type="text" placeholder="Email" />
      <input v-model="password" type="password" placeholder="Password" />
      <button type="submit">Login</button>
    </form>
  </div>
  <div v-if="errorMessage" class="error-message">{{ errorMessage }}</div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post("http://127.0.0.1:8000/api/login", {
          email: this.email,
          password: this.password,
        });

        // Store the JWT token in localStorage
        const token = response.data.access_token;
        localStorage.setItem("jwt_token", token);

        // Redirect the user to another page
        this.$router.push("/");
      } catch (error) {
        console.error("Login error:", error);
        // Handle authentication error
        this.errorMessage =
          "Authentication failed. Please check your email and password.";
      }
    },
  },
};
</script>
