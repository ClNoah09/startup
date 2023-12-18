<script setup>
const query = gql`
  query MyQuery {
    equipes {
      id
      nom
      pseudo
      poste
      description
      age
      createdAt
      publishedAt
      updatedAt
      slug
      image {
        url(
          transformation: {
            image: { resize: { fit: crop, height: 1024, width: 1024 } }
          }
        )
      }
    }
  }
`;

const equipes = ref();
const { data } = await useAsyncQuery(query);
console.log(data.value);
equipes.value = data.value.equipes;
</script>

<template>
  <ul
    v-if="equipes"
    class="flex justify-center list-none mx-auto space-x-4 mt-10"
  >
    <li
      v-for="equipe in equipes"
      :key="equipe.id"
      class="flex flex-col items-center border-4 border-yellow-500 rounded-lg w-full sm:w-48 lg:w-56 xl:w-64 2xl:w-72"
    >
      <NuxtLink
        :to="`/equipe/${equipe.slug}`"
        class="text-center transition-transform hover:scale-110"
      >
        <NuxtImg
          :src="equipe.image.url"
          :alt="equipe.nom"
          class="max-w-full h-auto border-b-2 border-black transition-transform transform-origin-center"
        />
        <h2 class="bg-green-800 text-yellow-500 text-xl sm:text-2xl py-2">
          {{ equipe.nom }}
        </h2>
      </NuxtLink>
    </li>
  </ul>

  <ul v-else>
    <li>Loading...</li>
  </ul>
</template>
