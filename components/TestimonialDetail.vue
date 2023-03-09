<template>
  <div
    v-if="showDetail"
    class="fixed inset-0 bg-white bg-opacity-90 z-50"
  >
    <div
      class="bg-white border-purple-700 border-2 w-80 rounded-lg shadow-lg"
    >
      <div class="relative">
        <div class="absolute top-0 left-1/2 transform -translate-x-1/2 -translate-y-1/2 rounded-full overflow-hidden w-20 h-20">
          <img :src="noTestimonyItem.avatar" alt="Person's photo" class="w-full h-full object-cover">
        </div>
      </div>
      <div class="p-4 mt-10 flex flex-col items-center justify-center">
        <p class="text-lg font-bold">{{ noTestimonyItem.name }} {{ noTestimonyItem.last_name }}</p>
        <p class="text-gray-600">{{ noTestimonyItem.profession }}</p>
      </div>
      <div v-if="!loadingTestimony">
        <div class="my-3 mx-3">
          <p>Testimony</p>
        </div>
        <div class="my-3 mx-3">
          <p class="text-justify">{{ testimony }}</p>
        </div>
        <div class="grid grid-cols-3 gap-4 mx-3 my-3">
          <a href="https://github.com/Talently-Oficial">
            <img src="~assets/images/iconmonstr-github-1.svg" alt="Github Profile" class="rounded-full h-12 w-24 items-center justify-center">
          </a>
          <a href="https://twitter.com/TalentlyTech">
            <img src="~assets/images/icons8-twitter.svg" alt="Twitter Profile"  class="rounded-full h-12 w-24 items-center justify-center">
          </a>
          <a href="https://www.linkedin.com/school/talentlytech">
            <img src="~assets/images/icons8-linkedin.svg" alt="Linkedin Profile"  class="rounded-full h-12 w-24 items-center justify-center">
          </a>
        </div>
      </div>
      <div v-if="loadingTestimony" class="mt-10 flex justify-center items-center">
        ...Loading
      </div>
      <div v-if="testimonyError" class="mt-10 flex justify-center items-center">
        ...Error on loading testimony
      </div>
    </div>
  </div>
</template>
<script setup>
  // props
  const props = defineProps({
    showDetail: {
      type: Boolean,
      default: false
    },
    noTestimonyItem: {
      type: Object,
      default: () => ({})
    }
  })

  // Manage Testimony Description Card
  const testimony = ref({})
  const loadingTestimony = ref(false)
  const testimonyError = ref(false)
  const indexedTestimony = ref({})
  const getUserDetail = ref(async (cardId) => {
    try {
      if (!cardId) return
      loadingTestimony.value = true
      // Checks if testimony is already fetched and stored in indexedTestimony
      if (!indexedTestimony[cardId]) {
        // If not fetched, fetches testimony from API
        const response = await useFetch(`https://api-challenge-talently.vercel.app/api/users/${cardId}`)
        if (response.data.value.success) {
          testimony.value = response.data.value.result.testimony
          indexedTestimony[cardId] = response.data.value.result.testimony
          loadingTestimony.value = false
        } else {
          loadingTestimony.value = false
          testimonyError.value = true
        }
      } else {
        // If fetched, uses testimony from indexedTestimony
        testimony.value = indexedTestimony[cardId]
        loadingTestimony.value = false
      }
    } catch (error) {
      loadingTestimony.value = true
    }
  })
  defineExpose({
    getUserDetail
  })
</script>
<style scoped>
:host {
  height: 12rem;
}

:host .relative {
  height: 5rem;
}

.fixed {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
</style>