<!-- eslint-disable vue/multi-word-component-names -->
vue
<template>
  <div :class="['max-w-md mx-auto mt-10 p-5 border rounded shadow', isDarkMode ? 'bg-gray-800 text-white' : 'bg-white text-black']">
    <h2 class="text-xl font-bold mb-4">Send Request to Admin</h2>
    <form @submit.prevent="sendRequest">
      <label for="username" class="block mb-2">Your Name:</label>
      <input
        type="text"
        id="username"
        v-model="username"
        required
        class="w-full p-2 border border-gray-300 rounded mb-4"
      />
      <label for="request" class="block mb-2">Request:</label>
      <textarea
        id="request"
        v-model="request"
        rows="4"
        required
        class="w-full p-2 border border-gray-300 rounded mb-4"
      ></textarea>
      <button
        type="submit"
        class="w-full p-2 bg-green-500 text-white rounded hover:bg-green-600"
      >
        Send Request
      </button>
    </form>
    <button @click="toggleDarkMode" class="mt-4 p-2 bg-blue-500 text-white rounded hover:bg-blue-600">
      Toggle Dark Mode
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const username = ref('');
const request = ref('');
const isDarkMode = ref(false);
const sendRequest = async () => {
  try {
    const response = await fetch('/send-request', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ username: username.value, request: request.value }),
    });
    if (response.ok) {
      alert('Request sent successfully!');
      username.value = '';
      request.value = '';
    } else {
      const errorData = await response.json();
      alert(`Failed to send request: ${errorData.message || 'Unknown error'}`);
    }
  } catch (error) {
    console.error('Error:', error);
    alert('An error occurred. Please try again later.');
  }
};
const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value;
};
</script>

<style>
body {
  font-family: Arial, Helvetica, sans-serif;
  transition: background-color 0.3s, color 0.3s;
}

.bg-gray-800 {
  background-color: #2d3748; /* Dark background color */
}

.bg-white {
  background-color: #ffffff; /* Light background color */
}

.text-white {
  color: #ffffff; /* Light text color */
}

.text-black {
  color: #000000; /* Dark text color */
}
</style>