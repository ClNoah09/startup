<script setup>
const query = gql`
  query blog($slug: String!) {
    blog(where: { slug: $slug }) {
      id
      titre
      contenue
      slug
      createdAt
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

const blog = ref();

const route = useRoute();
const { data } = await useAsyncQuery(query, {
  slug: route.params.slug,
});

console.log(data.value);
blog.value = data.value.blog;
</script>

<template>
  <div v-if="blog" class="bg-gray-900 text-white py-12">
    <div
      class="container mx-auto flex flex-col items-center justify-center space-y-8"
    >
      <h2
        class="text-4xl md:text-5xl font-extrabold text-yellow-500 bg-green-700 p-6 rounded-lg shadow-lg"
      >
        {{ blog.titre }}
      </h2>
      <div
        class="flex flex-col md:flex-row items-center md:items-stretch mt-10"
      >
        <div class="md:flex-1">
          <NuxtImg
            :src="blog.image.url"
            :alt="blog.nom"
            class="w-full h-auto rounded-lg shadow-md"
          />
        </div>
        <div
          class="md:flex-1 text-yellow-500 bg-green-700 p-6 rounded-lg shadow-md"
        >
          <p class="text-lg">{{ blog.contenue }}</p>
        </div>
      </div>
    </div>
  </div>

  <div v-else>
    <li>Loading...</li>
  </div>
</template>
