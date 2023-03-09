<template>
  <!-- Cards Grid List -->
  <div
    v-if="isFetching"
  >
    ...Loading
  </div>
  <div
    v-if="errorOnFetch"
  >
    ...Error on fetching data
  </div>
  <div v-if="!isFetching" class="md:grid grid-cols-3 gap-4 mt-32">
    <div
      v-for="card in cardItems"
      :key="card.id"
      class="bg-white border-1 rounded-lg flex p-4 cursor-pointer shadow-lg mt-5 mx-0 px-5 py-5"
      @click.stop="openDetail(card)"
    >
      <div class="w-1/4 flex justify-center items-center">
        <div class="rounded-full overflow-hidden w-20 h-20">
          <img :src="card.avatar" alt="Person's photo" class="w-full h-full object-cover">
        </div>
      </div>
      <div class="w-3/4 ml-4">
        <p class="text-lg font-bold">{{ card.name }} {{ card.last_name }}</p>
        <p class="text-gray-600">{{ card.profession }}</p>
      </div>
    </div>
  </div>
  <!-- End of Cards Grid List -->
  <TestimonialDetail
    ref="testimonialDetailRef"
    :show-detail="showDetailCard"
    :no-testimony-item="noTestimonyItem"
  />
  <AddTestimonial
    :show-add-testimonial="showAddTestimonial"
    @close-add-testimonial="$emit('close-add-testimonial')"
    @added-testimonial="addedTestimonial($event)"
  />
</template>
<script setup>
const getTestimonialsUrl = "https://api-challenge-talently.vercel.app/api/users"
const { data: apiResponse } = useFetch(getTestimonialsUrl)
const isFetching = ref(false)
const errorOnFetch = ref(false)
const cardItems = ref([])

const getTestimonials = ref(() => {
  isFetching.value = true
  if (!apiResponse.value.result) {
    isFetching.value = false
    errorOnFetch.value = true
    return
  }
  cardItems.value = apiResponse.value.result
  isFetching.value = false
})
defineExpose({
  getTestimonials
})
onMounted(() => {
  isFetching.value = true
  if (!apiResponse.value.result) {
    isFetching.value = false
    errorOnFetch.value = true
    return
  }
  cardItems.value = apiResponse.value.result
  isFetching.value = false
})

// Card Detail
const testimonialDetailRef = ref({})
const handleWindowClick = (e) => {
  // Closes the modal if clicked outside of it
  if (!e.target.closest('bg-white')) {
    closeDetail()
  }
}
const noTestimonyItem = ref({})
const cardId = ref("")
const showDetailCard = ref(false)
const openDetail = (card) => {
  cardId.value = card.id
  noTestimonyItem.value = card
  showDetailCard.value = true
  window.addEventListener('click', handleWindowClick)
  testimonialDetailRef.value.getUserDetail(cardId.value)
}
const closeDetail = () => {
  showDetailCard.value = false
  window.removeEventListener('click', handleWindowClick)
}

// Add Testimonial
defineProps({
  showAddTestimonial: {
    type: Boolean,
    default: false
  }
})
const addedTestimonial = (testimony) => {
  cardItems.value.push(testimony)
  emit('added-testimonial')
}
const emit = defineEmits(['closeAddTestimonial', 'addedTestimonial'])
</script>