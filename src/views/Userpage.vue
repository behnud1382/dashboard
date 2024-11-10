<!-- eslint-disable vue/multi-word-component-names -->
vue
<template>
  <div class="container mx-auto p-4">
    <h1 class="text-2xl font-bold mb-4">User Profile</h1>
    <div class="bg-white shadow-md rounded-lg p-6">
      <h2 class="text-xl font-semibold mb-2">{{ user.name }}</h2>
      <p class="text-gray-700 mb-4">Email: {{ user.email }}</p>
      <p class="text-gray-700">Joined: {{ user.joinedDate }}</p>
      <button @click="editProfile" class="mt-4 bg-blue-500 text-white px-4 py-2 rounded">
        Edit Profile
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const user = ref({
  name: 'John Doe',
  email: 'john.doe@example.com',
  joinedDate: '2023-01-01',
});

const editProfile = () => {
  // Logic for editing the profile
  console.log('Edit Profile Clicked');
};
</script>

<style scoped>
/* Add any additional styles here if needed */
</style>