<template>
  <section class="mx-5 px-5">
    <div class="fixed top-0 left-0 w-full bg-gray-100 px-9 mx-0 pb-10">
      <CustomHeader class="mt-5  bg-gray-100"/>
      <div class="flow-root">
        <h1 class="float-left text-3xl">
          Testimonials
        </h1>
        <button
          class="bg-purple-500 hover:bg-purple-700 float-right text-white font-bold py-2 px-4 rounded"
          @click="addTestimonial"
        >
          New
        </button>
      </div>
    </div>
    <TestimonialsGrid
      ref="testimonialGridRef"
      :show-add-testimonial="showAddTestimonial"
      @close-add-testimonial="closeAddTestimonial"
      @added-testimonial="addedTestimonial"
    />
  </section>
  <div
    v-if="showSuccessMessage"
    class="fixed bottom-0 left-0 w-full bg-green-500 text-white p-4 text-center"
    role="alert"
  >
    Testimonial added successfully
  </div>
</template>
<script setup>
const showAddTestimonial = ref(false)

const addTestimonial = () => {
  showAddTestimonial.value = true
}

const closeAddTestimonial = () => {
  showAddTestimonial.value = false
}

const showSuccessMessage = ref(false)
const testimonialGridRef = ref({})
const addedTestimonial = () => {
  showSuccessMessage.value = true
  setTimeout(() => {
    showSuccessMessage.value = false
  }, 3000)
}
</script>
