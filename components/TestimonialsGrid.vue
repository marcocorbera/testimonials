<template>
  <!-- Cards List -->
  <div class="md:grid grid-cols-3 gap-4">
    <div
      v-for="card in cards"
      :key="card.name"
      class="max-w-sm w-full lg_max-w-full lg:flex mx-5"
    >
      <div class="w-16 md:w-32 lg:w-48 grid grid-cols-2 gap-4 my-5 border-black">
        <img :src="card.avatar" alt="Avatar Photo">
        <div class="grid grid-rows-2 gap-4">
          <div class="text-xs">
            {{ card.name }} {{ card.last_name }}
          </div>
          <div class="text-xs">
            {{ card.profession }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
const cards = reactive([
        {
            id: "AvbkEYDuh3ZjyGHRN5lT",
            avatar: "https://static-talently.s3.amazonaws.com/francisco_farfan_18754b3fed.jpg",
            name: "Francisco",
            last_name: "Farfán",
            profession: "Ingeniero de Software Full-Stack",
            github: "https://github.com/Talently-Oficial",
            twitter: "https://twitter.com/TalentlyTech",
            linkedin: "https://www.linkedin.com/school/talentlytech",
            company_logo: "https://static-talently.s3.amazonaws.com/rappi_8fbc74f632.png"
        },
        {
            id: "AxhS0b1KrJXdhaGsW40D",
            avatar: "https://static-talently.s3.amazonaws.com/1606680003693_9c9e44a1a8.jfif",
            name: "Lucas",
            last_name: "Amilivia",
            profession: "Ingeniero de Software",
            github: "https://github.com/Talently-Oficial",
            twitter: "https://twitter.com/TalentlyTech",
            linkedin: "https://www.linkedin.com/school/talentlytech",
            company_logo: "https://static-talently.s3.amazonaws.com/rappi_8fbc74f632.png"
        },
        {
            id: "JbYse3nPX4QPlKnKc7vK",
            avatar: "https://static-talently.s3.amazonaws.com/francisco_farfan_18754b3fed.jpg",
            name: "Francisco",
            last_name: "Farfán",
            profession: "Ingeniero de Software Full-Stack",
            github: "https://github.com/Talently-Oficial",
            twitter: "https://twitter.com/TalentlyTech",
            linkedin: "https://www.linkedin.com/school/talentlytech",
            company_logo: "https://static-talently.s3.amazonaws.com/rappi_8fbc74f632.png"
        },
        {
            id: "YGuA8b5249UMjovykvGQ",
            avatar: "https://static-talently.s3.amazonaws.com/leonardo_rivera_dd23565e2b.webp",
            name: "Leonardo",
            last_name: "Rivera",
            profession: "Desarrollador Angular",
            github: "https://github.com/Talently-Oficial",
            twitter: "https://twitter.com/TalentlyTech",
            linkedin: "https://www.linkedin.com/school/talentlytech",
            company_logo: "https://static-talently.s3.amazonaws.com/rappi_8fbc74f632.png"
        }
    ])
</script>