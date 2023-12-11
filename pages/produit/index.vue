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

<template></template>
