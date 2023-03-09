<template>
  <div
    v-if="showAddTestimonial"
    class="fixed inset-0 bg-white bg-opacity-90 z-50 px-4 py-36"
  >
    <div class="bg-white border-purple-700 border-2 rounded-lg shadow-lg">
      <div class="mx-5 my-5">
        <h1 class="mb-5">
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
              <input id="image-url" type="text" class="w-full border border-grey-900 rounded-md" v-model="avatar" @change="loadImage">
              <div v-if="avatarError" class="invalid-feedback">{{ avatarError }}</div>
            </div>
          </div>
  
          <!-- Second row -->
          <div class="flex space-x-4">
            <div class="flex-1">
              <label for="first-name">First Name</label>
              <input id="first-name" type="text" class="w-full border border-grey-900 rounded-md" v-model="firstName">
              <div v-if="firstNameError" class="invalid-feedback">{{ firstNameError }}</div>
            </div>
            <div class="flex-1">
              <label for="last-name">Last Name</label>
              <input id="last-name" type="text" class="w-full border border-grey-900 rounded-md" v-model="lastName">
              <div v-if="lastNameError" class="invalid-feedback">{{ lastNameError }}</div>
            </div>
          </div>
  
          <!-- Third row -->
          <div class="flex items-center space-x-4">
            <div class="w-1/2">
              <label for="profession">Profession</label>
              <input id="profession" type="text" class="w-full border border-grey-900 rounded-md" v-model="profession">
              <div v-if="professionError" class="invalid-feedback">{{ professionError }}</div>
            </div>
            <div class="w-1/2"></div>
          </div>
  
          <!-- Fourth row -->
          <div class="flex flex-col">
            <label for="testimony">Testimony</label>
            <textarea id="testimony" class="w-full border border-grey-900 rounded-md" v-model="testimony"></textarea>
            <div v-if="testimonyError" class="invalid-feedback">{{ testimonyError }}</div>
          </div>
  
          <!-- Fifth row -->
          <div class="flex justify-between">
            <button class="text-gray-500 hover:text-gray-700" @click.prevent="cancel()">Cancel</button>
            <button class="bg-purple-600 text-white px-4 py-2 rounded-md hover:bg-purple-700" @click.prevent="AddTestimonial">Add</button>
          </div>
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

const addTestimonialUrl = "https://api-challenge-talently.vercel.app/api/users/add"

// Data Values
const avatar = ref("")
const firstName = ref("")
const lastName = ref("")
const profession = ref("")
const testimony = ref("")
const avatarError = ref("")
const firstNameError = ref("")
const lastNameError = ref("")
const professionError = ref("")
const testimonyError = ref("")
const imageLoaded = ref(false)

// Manage Image preview
const loadImage = () => {
  imageLoaded.value = false
  const img = new Image()
  img.onload = () => {
    imageLoaded.value = true
  }
  img.src = avatar.value
}

const resetInputValues = () => {
  avatar.value = ""
  firstName.value = ""
  lastName.value = ""
  profession.value = ""
  testimony.value = ""
  imageLoaded.value = false
}

const emit = defineEmits(['close-add-testimonial', 'added-testimonial'])
const cancel = () => {
  emit('close-add-testimonial')
  resetInputValues()
}


const AddTestimonial = async () => {
  if (!firstName.value) {
    firstNameError.value = 'Name is required'
  } else {
    firstNameError.value = ""
  }
  if (!lastName.value) {
    lastNameError.value = 'Last name is required'
  } else {
    lastNameError.value = ""
  }
  if (!profession.value) {
    professionError.value = 'Profession is required'
  } else {
    professionError.value = ""
  }
  if (!testimony.value) {
    testimonyError.value = 'Testimony is required'
  } else {
    testimonyError.value = ""
  }
  if (!avatar.value) {
    avatarError.value = 'Avatar is required'
  } else {
    avatarError.value = ""
  }
  if (
    !firstName.value ||
    !lastName.value ||
    !profession.value ||
    !testimony.value ||
    !avatar.value
  ) {
    alert('Please fill all the fields before adding a new testimonial')
    return
  }
  const newTestimonial = {
    avatar: avatar.value,
    name: firstName.value,
    last_name: lastName.value,
    profession: profession.value,
    testimony: testimony.value
  }
  try {
    const response = await fetch(addTestimonialUrl, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(newTestimonial)
    })
    const data = await response.json()
    if (data.success) {
      resetInputValues()
      newTestimonial.id = data.id
      emit('added-testimonial', newTestimonial)
      emit('close-add-testimonial')
    } else {
      alert('We could not add the testimonial, please try again later')
    }
  } catch (e) {
    alert('We could not add the testimonial, please contact support')
  }

}
</script>
<style scoped>
.invalid-feedback {
  color: red;
}
</style>