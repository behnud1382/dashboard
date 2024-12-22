<script setup>
import { ref, computed } from 'vue';
import { useAuthStore } from '@/stores/authStore'; // فرض بر این است که نقش کاربر در اینجا ذخیره شده

const authStore = useAuthStore();
const isSidebarVisible = ref(true); // متغیر برای مدیریت نمایش سایدبار

// تعریف آیتم‌های منو بر اساس نقش کاربر
const menuItems = computed(() => {
  if (authStore.role === 'admin') {
    return [
      { link: '/', name: 'Dashboard', tooltip: 'Dashboard', icon: 'bx-grid-alt' },
      { link: '/admincalendar', name: 'Admin Calendar', tooltip: 'Admin Calendar', icon: 'bx-calendar' },
      { link: '/usermanagement', name: 'User Management', tooltip: 'User Management', icon: 'bx-user' },
      { link: '/settings', name: 'Settings', tooltip: 'Settings', icon: 'bx-cog' },
      { link: '/faq', name: 'Faq', tooltip: 'Faq', icon: 'bx-faq' },
    ];
  } else if (authStore.role === 'user') {
    return [
      { link: '/', name: 'Dashboard', tooltip: 'Dashboard', icon: 'bx-grid-alt' },
      { link: '/calendar', name: 'Calendar', tooltip: 'Calendar', icon: 'bx-calendar' },
      { link: '/settings', name: 'Settings', tooltip: 'Settings', icon: 'bx-cog' },
      { link: '/faq', name: 'Faq', tooltip: 'Faq', icon: 'bx-faq' },
    ];
  }
  return [];
});

// تابع برای تغییر وضعیت نمایش سایدبار
const toggleSidebar = () => {
  isSidebarVisible.value = !isSidebarVisible.value;
};
</script>

<template>
  <div class="layout">
    <!-- دکمه نمایش/مخفی‌سازی سایدبار -->
    <button class="toggle-button" @click="toggleSidebar">
      <i :class="isSidebarVisible ? 'bx bx-chevron-left' : 'bx bx-chevron-right'"></i>
    </button>

    <!-- سایدبار -->
    <nav v-show="isSidebarVisible" class="sidebar">
      <ul>
        <li v-for="item in menuItems" :key="item.name">
          <router-link :to="item.link" class="flex items-center gap-2">
            <i :class="item.icon"></i>
            <span>{{ item.name }}</span>
          </router-link>
        </li>
      </ul>
    </nav>

    <!-- محتوای اصلی -->
    <main class="main-content">
      <router-view />
    </main>
  </div>
</template>

<style scoped>
.layout {
  display: flex;
  height: 100vh;
}

/* استایل سایدبار */
.sidebar {
  width: 250px;
  background-color: #1a202c;
  color: white;
  padding: 1rem;
  transition: transform 0.3s ease-in-out;
}

.sidebar ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.sidebar li {
  margin-bottom: 1rem;
}

.sidebar a {
  text-decoration: none;
  color: white;
  display: flex;
  align-items: center;
}

.sidebar a:hover {
  color: #63b3ed;
}

/* استایل دکمه نمایش/مخفی‌سازی */
.toggle-button {
  background: #1a202c;
  color: white;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
  position: fixed;
  top: 1rem;
  left: 1rem;
  z-index: 1000;
}

.toggle-button i {
  font-size: 1.5rem;
}

/* استایل محتوای اصلی */
.main-content {
  flex: 1;
  padding: 1rem;
  background-color: #f7fafc;
}
</style>