<template>
  <section class="mx-5 px-5">
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
    <TestimonialsGrid
      :show-add-testimonial="showAddTestimonial"
      @close-add-testimonial="closeAddTestimonial"
    />
  </section>
</template>
<script setup>
const showAddTestimonial = ref(false)
const addTestimonial = () => {
  showAddTestimonial.value = true
}
const closeAddTestimonial = () => {
  showAddTestimonial.value = false
}
</script>
