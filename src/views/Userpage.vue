<!-- eslint-disable vue/multi-word-component-names -->
eslint-disable-next-line vue/multi-word-component-names
<template>
  <div class="max-w-md mx-auto mt-10 p-5 border rounded shadow">
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
  </div>
</template>

<script setup>
import { ref } from 'vue';

const username = ref('');
const request = ref('');

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
</script>

<style>
/* You can add additional styles here if needed */
</style>