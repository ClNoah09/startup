<script setup>
const query = gql`
  query MyQuery {
    societes {
      id
      slug
      titre
      contenue
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

const societes = ref();
const { data } = await useAsyncQuery(query);
console.log(data.value);
societes.value = data.value.societes;
</script>

<template>
  <div
    v-for="societe in societes"
    :key="societe.id"
    class="bg-gray-900 text-white min-h-screen flex flex-col justify-center items-center"
  >
    <h2 class="text-4xl md:text-5xl font-extrabold text-yellow-500 mb-4">
      {{ societe.titre }}
    </h2>
    <div class="mb-8">
      <NuxtImg
        :src="societe.image.url"
        :alt="societe.titre"
        class="w-full h-auto rounded-lg shadow-md"
      />
    </div>
    <div class="text-yellow-500 bg-green-700 p-4 rounded-lg shadow-md">
      <p class="text-lg">{{ societe.contenue }}</p>
    </div>
  </div>
</template>
