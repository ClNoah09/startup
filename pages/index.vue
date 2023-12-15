<script setup>
const query = gql`
  query Page {
    page(where: { slug: "accueil" }) {
      createdAt
      id
      publishedAt
      slug
      titre
      updatedAt
      text {
        html
      }
    }
  }
`;

const contenueAccueil = ref();
const { data } = await useAsyncQuery(query);
console.log(data.value.page.text);
contenueAccueil.value = data.value.page;
</script>

<template>
  <div
    id="fonds"
    class="min-h-screen bg-cover"
    style="
      background-image: url('/public/img/challenger-se-tient-devant-illustration-effrayante-du-chateau.jpg');
    "
  >
    <div class="flex flex-col items-center justify-center h-full text-white">
      <h1 class="text-yellow-500 text-6xl font-bold mb-8">
        Bienvenue chez LevelLoot
      </h1>
      <div class="flex space-x-4">
        <a
          href="/produit"
          class="bg-green-950 text-yellow-500 border-2 border-yellow-500 px-4 py-2 rounded-lg"
          >Services</a
        >
        <a
          href="/contact"
          class="bg-green-950 text-yellow-500 border-2 border-yellow-500 px-4 py-2 rounded-lg"
          >Contact</a
        >
      </div>
      <div class="bg-green-950 bg-opacity-70">
        <p
          v-html="contenueAccueil.text.html"
          class="text-yellow-500 text-stroke text-center text-lg p-4 inline-block"
        ></p>
      </div>

      <!-- Gallery of photos -->
      <div class="grid grid-cols-3 gap-4 mt-8">
        <img
          src="../public/img/OIG (9).jpg"
          alt="Image 1"
          class="w-full h-auto rounded"
        />
        <img
          src="../public/img/OIG.jpg"
          alt="Image 2"
          class="w-full h-auto rounded"
        />
        <img
          src="../public/img/OIG (1).jpg"
          alt="Image 3"
          class="w-full h-auto rounded"
        />
        <!-- Add more images as needed -->
      </div>
    </div>
  </div>
</template>
