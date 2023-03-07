<template>
  <section class="mx-5 pt-5">
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
    <TestimonialsGrid class="mt-5" />
  </section>
</template>
<script setup>
const addTestimonial = () => {
  console.log('addTestimonial')
}
</script>
