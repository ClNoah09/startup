<script setup>
const query = gql`
  query produit {
    produit(where: { slug: "$slug" }) {
      nom
      slug
      description
      createdAt
      publishedAt
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

const contenueProduit = ref();
const { data } = await useAsyncQuery(query);
console.log(data.value);
contenueProduit.value = data.value.produit;
</script>

<template>
  <ul
    v-if="produit"
    class="grid gap-8 grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 2xl:grid-cols-6"
  >
    <li
      v-for="produit in produits"
      :key="produit.id"
      class="flex flex-col items-center border-4 border-red-500 rounded-lg w-fit"
    >
      <NuxtLink
        :to="`/produit/${produit.slug}`"
        class="text-center transition-transform hover:scale-110"
      >
        <NuxtImg
          :src="produit.image.url"
          :alt="produit.nom"
          class="max-w-full h-auto border-b-2 border-black hover:border-red-500 transition-transform transform-origin-center"
        />
        <h2 class="bg-white text-2xl py-2">{{ produit.nom }}</h2>
      </NuxtLink>
    </li>
  </ul>
  <ul v-else>
    <li>Loading...</li>
  </ul>
</template>
