vue
<template>
  <form @submit.prevent="handleSubmit" class="max-w-md mx-auto p-6 bg-white rounded-lg shadow-md">
    <h3 class="text-xl font-semibold mb-4">Forget Password</h3>
    <div class="mb-4">
      <label class="block text-gray-700 text-sm font-bold mb-2">Email</label>
      <input 
        type="email" 
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
        v-model="email" 
        placeholder="Email" 
        required 
      />
    </div>
    <button 
      class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
    >
      Submit
    </button>
  </form>
</template>

<script>
import axios from 'axios' 

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Forgot',
  data() {
    return {
      email: ''
    }
  },
  methods: {
    async handleSubmit() {
      try {
        const response = await axios.post('forget', {
          email: this.email
        }); 
        console.log(response);
      } catch (error) {
        console.error("There was an error!", error);
      }
    }
  },
}
</script>