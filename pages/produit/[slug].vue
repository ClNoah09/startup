<script setup>
const query = gql`
  query produit($slug: String!) {
    produit(where: { slug: $slug }) {
      id
      nom
      slug
      description
      createdAt
      publishedAt
      updatedAt
      stage
      prix
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

const produit = ref();

const route = useRoute();
const { data } = await useAsyncQuery(query, {
  slug: route.params.slug,
});

console.log(data.value);
produit.value = data.value.produit;
</script>

<template>
  <div v-if="produit" class="text-white py-12">
    <div class="max-w-4xl mx-auto flex flex-col items-center space-y-8">
      <h2
        class="text-3xl md:text-4xl text-center font-bold text-yellow-500 bg-green-700 p-4 rounded-lg shadow-lg"
      >
        {{ produit.nom }}
      </h2>
      <div
        class="flex flex-col md:flex-row items-center md:items-stretch mt-10"
      >
        <div class="md:flex-1">
          <NuxtImg
            :src="produit.image.url"
            :alt="produit.nom"
            class="w-full h-auto rounded-lg shadow-md"
          />
        </div>
        <div
          class="md:flex-1 text-yellow-500 bg-green-700 p-4 rounded-lg shadow-md"
        >
          <p class="text-lg mb-4">{{ produit.description }}</p>
          <p class="text-2xl font-bold">{{ produit.prix }}€</p>
        </div>
      </div>
    </div>
  </div>

  <div v-else>
    <li>Loading...</li>
  </div>
</template>
