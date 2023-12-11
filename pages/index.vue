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
  <h2>
    {{ contenueAccueil.titre }}
  </h2>

  <div v-html="contenueAccueil.text.html"></div>
</template>
