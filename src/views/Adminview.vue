<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="flex h-screen">
    <!-- Sidebar -->
    <aside class="bg-gray-800 text-white w-64 p-4">
      <h2 class="text-lg font-bold mb-4">Menu</h2>
      <ul>
        <li
          v-for="item in menuItems"
          :key="item.name"
          class="mb-2"
        >
          <a
            :href="item.link"
            class="block hover:bg-gray-700 rounded p-2 flex items-center"
          >
            <span class="mr-2">{{ item.icon }}</span> <!-- Icon if available -->
            {{ item.name }}
          </a>
        </li>
      </ul>
    </aside>

    <!-- Main Content -->
    <main class="flex-1 bg-gray-100 p-6">
      <h1 class="text-2xl font-bold mb-4">Welcome, {{ role }}</h1>
      <p class="text-gray-700">Here is the content based on your role.</p>
    </main>
  </div>
</template>

<script setup>
import { ref } from "vue";

// Mock user role (to be replaced with actual role fetching logic)
const role = ref("admin"); // Change this to "user" to test user-specific view

// Dynamic menu based on user role
const adminMenu = [
  { name: "Dashboard", link: "/dashboard", icon: "📊" },
  { name: "Calendar", link: "/calendar", icon: "📅" },
  { name: "AdminCalendar", link: "/admincalendar", icon: "🗓️" },
  { name: "UserManagement", link: "/usermanagement", icon: "👥" },
];

const userMenu = [
  { name: "Dashboard", link: "/dashboard", icon: "📊" },
  { name: "Calendar", link: "/calendar", icon: "📅" },
];

// Set the menu items dynamically based on the role
const menuItems = ref(role.value === "admin" ? adminMenu : userMenu);
</script>

<style scoped>
/* Additional styling if needed */
</style>
