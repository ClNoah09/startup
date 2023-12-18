<script setup>
const query = gql`
  query Blogs {
    blogs {
      id
      titre
      slug
      contenue
      publishedAt
      updatedAt
      createdAt
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

const blogs = ref();
const { data } = await useAsyncQuery(query);
console.log(data.value);
blogs.value = data.value.blogs;
</script>

<template>
  <h2 class="text-center text-4xl text-yellow-500 underline">
    Dernières nouvelles
  </h2>

  <ul v-if="blogs" class="flex flex-col items-center list-none mx-auto mt-10">
    <li
      v-for="blog in blogs"
      :key="blog.id"
      class="flex flex-col sm:flex-row items-center rounded-lg w-full sm:w-48 lg:w-56 xl:w-64 2xl:w-72 mb-4 bg-green-800"
    >
      <NuxtLink
        :to="`/blog/${blog.slug}`"
        class="text-center transition-transform flex flex-col items-center mg-10 line-height-2"
      >
        <h2 class="text-yellow-500 text-xl sm:text-2xl py-2 line-clamp-2">
          {{ blog.titre }}
        </h2>
        <NuxtImg
          :src="blog.image.url"
          :alt="blog.titre"
          class="max-w-full h-auto transition-transform transform-origin-center"
        />
      </NuxtLink>
    </li>
  </ul>

  <ul v-else>
    <li>Loading...</li>
  </ul>
</template>
