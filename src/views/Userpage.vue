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

<script>
import axios from 'axios';

export default {
  data() {
    return {
      user: null,
      fetchError: null // Added to store error messages
    };
  },
  mounted() {
    // Fetch user data from API
    axios.get('/api/user')
      .then(response => {
        // Log the response for debugging
        console.log('Response from API:', response);
        // Check if the response data is in the expected format
        if (response.data && response.data.name && response.data.email) {
          this.user = response.data;
        } else {
          this.fetchError = 'Unexpected response format.';
        }
      })
      .catch(error => {
        console.error('Error fetching user data:', error);
        // Provide more detailed error information
        this.fetchError = (error.response && error.response.data && error.response.data.message) 
          ? error.response.data.message 
          : 'Failed to load user data. Please try again later.'; // Set error message
      });
  }
};
</script>