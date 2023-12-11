<script setup>
const props = defineProps({
  to: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <NuxtLink
    :to="to"
    class="text-lg text-[#d6ae2f] hover:text-[#d6d3ae] hover:underline transition"
    active-class="font-bold"
  >
    <slot />
  </NuxtLink>
</template>
