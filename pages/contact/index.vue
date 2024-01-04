<script setup>
const query = gql`
  query MyQuery {
    contacts {
      id
      titre
      contenue
      email
      slug
      numero
      adresse
      createdAt
      publishedAt
      updatedAt
    }
  }
`;

const contacts = ref();
const { data } = await useAsyncQuery(query);
console.log(data.value);
contacts.value = data.value.contacts;
</script>

<template>
  <div
    v-for="contact in contacts"
    :key="contact.id"
    class="bg-gray-900 text-red min-h-screen flex flex-col justify-center items-center"
  >
    <h2 class="text-4xl md:text-5xl font-extrabold text-yellow-500 mb-4">
      {{ contact.titre }}
    </h2>
    <div class="mb-8">
      <div class="text-yellow-500 bg-green-700 p-4 rounded-lg shadow-md">
        <p class="text-lg">{{ contact.contenue }}</p>
      </div>
    </div>
    <form class="max-w-xl mx-auto p-6 bg-white rounded-md shadow-md">
      <div class="mb-4">
        <label for="name" class="block text-gray-700 text-sm font-semibold mb-2"
          >Nom :</label
        >
        <input
          type="text"
          id="name"
          name="name"
          required
          class="w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:border-blue-500 placeholder-gray-500"
          placeholder="Votre nom"
        />
      </div>

      <div class="mb-4">
        <label
          for="email"
          class="block text-gray-700 text-sm font-semibold mb-2"
          >Email :</label
        >
        <input
          type="email"
          id="email"
          name="email"
          required
          class="w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:border-blue-500 placeholder-gray-500"
          placeholder="Votre adresse email"
        />
      </div>

      <div class="mb-4">
        <label
          for="message"
          class="block text-gray-700 text-sm font-semibold mb-2"
          >Message :</label
        >
        <textarea
          id="message"
          name="message"
          rows="4"
          required
          class="w-full border border-gray-300 rounded-md px-3 py-2 resize-none focus:outline-none focus:border-blue-500 placeholder-gray-500"
          placeholder="Votre message"
        ></textarea>
      </div>

      <button
        type="submit"
        class="bg-blue-500 text-white py-2 px-4 rounded-md hover:bg-blue-600 focus:outline-none focus:shadow-outline-blue"
      >
        Envoyer
      </button>
    </form>

    <p class="text-[#d6d3ae] text-lg">{{ contact.adresse }}</p>
    <p class="text-[#d6d3ae] text-lg">{{ contact.email }}</p>
    <p class="text-[#d6d3ae] text-lg">0{{ contact.numero }}</p>
  </div>
</template>
