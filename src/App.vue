<template>
  <div class="container">
    <h1>Sign Our Petition</h1>
    <p>Your support means everything! Join us in making a difference.</p>

    <button class="btn-red" @click="signPetition">Sign the Petition</button>

    <p class="disclaimer">* We will collect only your IP Address once you click.</p>

    <!-- Show success message -->
    <p v-if="successMessage" class="success">{{ successMessage }}</p>

    <!-- Show error message -->
    <p v-if="errorMessage" class="error">{{ errorMessage }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      successMessage: '',
      errorMessage: '',
      signedIPs: [],
    };
  },
  methods: {
    async signPetition() {
      try {
        // Make a request to a public IP API to get the user's IP address
        const response = await axios.get('https://api.ipify.org?format=json');
        const userIP = response.data.ip;

        // Mock store the IP address (for demonstration purposes, we push it to an array)
        // In a real application, you'd send it to your server to save in a database
        this.signedIPs.push(userIP);

        // Show success message
        this.successMessage = `Thank you for signing the petition! Your IP: ${userIP}`;
        this.errorMessage = '';
      } catch (error) {
        this.errorMessage = 'There was a problem signing the petition. Please try again.';
        this.successMessage = '';
      }
    },
  },
};
</script>

<style>
html, body {
  height: 100%;
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial, sans-serif;
  background: white !important;
  color: black !important;
}

.container {
  text-align: center;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.btn-red {
  background-color: red;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  margin-top: 20px;
  border-radius: 5px;
}

.btn-red:hover {
  background-color: darkred;
}

.disclaimer {
  color: #6c757d;
  font-size: 12px;
  margin-top: 10px;
}

.success {
  color: green;
  margin-top: 20px;
}

.error {
  color: red;
  margin-top: 20px;
}
</style>
