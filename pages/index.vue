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
      <h1 class="text-6xl font-bold mb-8">Bienvenue au Château Effrayant</h1>
      <div class="flex space-x-4">
        <a href="/services" class="bg-blue-500 text-white px-4 py-2 rounded"
          >Services</a
        >
        <a href="/contact" class="bg-green-500 text-white px-4 py-2 rounded"
          >Contact</a
        >
      </div>
      <p class="mt-8 text-lg text-center">
        Découvrez l'atmosphère unique de notre château effrayant. Vous ne
        trouverez rien de semblable ailleurs!
      </p>

      <!-- Gallery of photos -->
      <div class="grid grid-cols-3 gap-4 mt-8">
        <img
          src=""
          alt="Image 1"
          class="w-full h-auto rounded"
        />
        <img
          src=""
          alt="Image 2"
          class="w-full h-auto rounded"
        />
        <img
          src=""
          alt="Image 3"
          class="w-full h-auto rounded"
        />
        <!-- Add more images as needed -->
      </div>
    </div>
  </div>
</template>
