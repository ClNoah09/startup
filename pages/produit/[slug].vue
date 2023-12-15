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
    class="max-w-xl mx-auto flex flex-col md:flex-row items-center justify-center space-x-3"
  >
    <div class="flex-1 mt-10">
      <NuxtImg
        :src="produit.image.url"
        :alt="produit.nom"
        class="w-full h-auto"
      />
    </div>
    <div class="flex-1 text-center text-yellow-500">
      <h2 class="text-4xl bg-green-800 bg-opacity-50">{{ produit.nom }}</h2>
      <p class="text-lg bg-green-800 bg-opacity-50">
        {{ produit.description }}
      </p>
      <p class="text-lg bg-green-800 bg-opacity-50">{{ produit.prix }}€</p>
    </div>
  </div>

  <div v-else>
    <li>Loading...</li>
  </div>
</template>
