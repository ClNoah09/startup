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
  <div
    v-if="produit"
    class="max-w-xl mx-auto flex flex-col items-center justify-center space-x-4 bg-green-800 bg-opacity-50"
  >
    <h2 class="text-4xl text-center text-yellow-500">{{ produit.nom }}</h2>
    <div class="flex mt-10">
      <div class="flex-1">
        <NuxtImg
          :src="produit.image.url"
          :alt="produit.nom"
          class="w-full h-auto"
        />
      </div>
      <div class="flex-1 text-center text-yellow-500">
        <p class="text-lg">{{ produit.description }}</p>
        <p class="text-lg">{{ produit.prix }}€</p>
      </div>
    </div>
  </div>

  <div v-else>
    <li>Loading...</li>
  </div>
</template>
