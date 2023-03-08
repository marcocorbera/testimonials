<template>
  <div
    v-if="showAddTestimonial"
    class="fixed inset-0 bg-white bg-opacity-90 z-50"
  >
    <div class="bg-white border-purple-700 border-2 min-w-modal rounded-lg shadow-lg">
      <h1>
        New Testimony
      </h1>
      <div class="flex flex-col space-y-4">
        <!-- First row -->
        <div class="flex items-center space-x-4">
          <div v-if="!imageLoaded" class="w-12 h-12 rounded-full bg-gray-300"></div>
          <div v-else class="w-12 h-12 rounded-full overflow-hidden">
            <img :src="avatar" alt="Person's photo" class="w-full h-full object-cover">
          </div>
          <div class="flex-1">
            <label for="image-url">Avatar URL</label>
            <input id="image-url" type="text" class="w-full border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-600" v-model="avatar">
          </div>
        </div>

        <!-- Second row -->
        <div class="flex space-x-4">
          <div class="flex-1">
            <label for="first-name">First Name</label>
            <input id="first-name" type="text" class="w-full border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-600" v-model="firstName">
          </div>
          <div class="flex-1">
            <label for="last-name">Last Name</label>
            <input id="last-name" type="text" class="w-full border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-600" v-model="lastName">
          </div>
        </div>

        <!-- Third row -->
        <div class="flex items-center space-x-4">
          <div class="w-1/2">
            <label for="profession">Profession</label>
            <input id="profession" type="text" class="w-full border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-600" v-model="profession">
          </div>
          <div class="w-1/2"></div>
        </div>

        <!-- Fourth row -->
        <div class="flex flex-col">
          <label for="testimony">Testimony</label>
          <textarea id="testimony" class="w-full border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-600" v-model="testimony"></textarea>
        </div>

        <!-- Fifth row -->
        <div class="flex justify-between">
          <button class="text-gray-500 hover:text-gray-700" @click.prevent="cancel()">Cancel</button>
          <button class="bg-purple-600 text-white px-4 py-2 rounded-md hover:bg-purple-700" @click.prevent="add()">Add</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
defineProps({
  showAddTestimonial: {
    type: Boolean,
    default: false
  }
})

const avatar = ref('')
const firstName = ref('')
const lastName = ref('')
const profession = ref('')
const testimony = ref('')
const imageLoaded = ref(false)
</script>