<!-- eslint-disable vue/multi-word-component-names -->
vue
<template>
  <div>
    <div class="h-screen bg-dark-500 flex items-center justify-center dark:text-white ">
      <form @submit.prevent="sendRequest">
        <label for="username" class="block mb-2">Your Name:</label>
        <input
          type="text"
          id="username"
          v-model="username"
          required
          class="w-full p-2 text-sm border rounded-lg dark:bg-gray-700 dark:border-gray-600"
        />
        <label for="request" class="block mb-2 dark-mode">Request:</label>
        <textarea
          id="request"
          v-model="request"
          rows="4"
          required
          class="w-full p-2 text-sm border rounded-lg dark:bg-gray-700 dark:bordr-gray-600"
        ></textarea>
        <button
          type="submit"
          class="w-full p-2 bg-green-500 text-white rounded hover:bg-green-600"
        >
          Send Request
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const username = ref('');
const request = ref('');
async function sendRequest() {
    try {
        const apiUrl = 'https://example.com/api/requests';
        const payload = {
            username: username.value,
            request: request.value,
        };
        const response = await fetch(apiUrl, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(payload),
        });
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        const data = await response.json();
        console.log('Response:', data);
        username.value = '';
        request.value = '';
        alert('Request sent successfully!');
    } catch (error) {
        console.error('Error sending request:', error);
        alert('Failed to send request. Please try again.');
    }
}
</script>

<style>
body.dark-mode {
  background-color: #2d3748; /* Dark background */
  color: black; /* Light text color */
}
.dark-text label {
  color: black;
}
</style>