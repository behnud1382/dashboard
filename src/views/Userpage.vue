<!-- eslint-disable vue/multi-word-component-names -->
vue
<template>
  <div class="user-page p-6 max-w-md mx-auto bg-white rounded-lg shadow-md">
    <h2 class="text-2xl font-semibold mb-4">User Profile</h2>
    <div v-if="user">
      <p class="text-lg">Name: <span class="font-medium">{{ user.name }}</span></p>
      <p class="text-lg">Email: <span class="font-medium">{{ user.email }}</span></p>
    </div>
    <div v-else-if="fetchError">
      <p class="text-red-500">Error fetching user data: {{ fetchError }}</p>
    </div>
    <div v-else>
      <p class="text-gray-500">Loading user data...</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const user = ref(null);
const fetchError = ref(null);

onMounted(async () => {
  try {
    const response = await axios.get('/api/user');
    console.log('Response from API:', response);

    if (response.data && response.data.name && response.data.email) {
      user.value = response.data;
    } else {
      fetchError.value = 'Unexpected response format.';
    }
  } catch (error) {
    console.error('Error fetching user data:', error);
    fetchError.value = (error.response && error.response.data && error.response.data.message) 
      ? error.response.data.message 
      : 'Failed to load user data. Please try again later.';
  }
});
</script>

<style scoped>
/* Add any additional styles here if needed */
</style>