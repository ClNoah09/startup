<script setup>
const query = gql`
  query MyQuery($slug: String!) {
    equipe(where: { slug: $slug }) {
      id
      nom
      pseudo
      poste
      age
      description
      createdAt
      slug
      publishedAt
      updatedAt
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

const equipe = ref();

const route = useRoute();
const { data } = await useAsyncQuery(query, {
  slug: route.params.slug,
});

console.log(data.value);
equipe.value = data.value.equipe;
</script>

<template>
  <div v-if="equipe" class="text-white py-12">
    <div class="max-w-4xl mx-auto flex flex-col items-center space-y-8">
      <h2
        class="text-3xl md:text-4xl text-center font-bold text-yellow-500 bg-green-700 p-4 rounded-lg shadow-lg"
      >
        {{ equipe.nom }} ({{ equipe.pseudo }})
      </h2>
      <div
        class="flex flex-col md:flex-row items-center md:items-stretch mt-10"
      >
        <div class="md:flex-1">
          <NuxtImg
            :src="equipe.image.url"
            :alt="equipe.nom"
            class="w-full h-auto rounded-lg shadow-md"
          />
        </div>
        <div
          class="md:flex-1 text-yellow-500 bg-green-700 p-4 rounded-lg shadow-md"
        >
          <p class="text-lg mb-4">{{ equipe.description }}</p>
          <p class="text-2xl font-bold">{{ equipe.prix }}</p>
        </div>
      </div>
    </div>
  </div>

  <div v-else>
    <li>Loading...</li>
  </div>
</template>
