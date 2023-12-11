<script setup>
defineProps({
  to: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <NuxtLink
    :to="to"
    class="text-[#d6ae2f] hover:text-[#d6d3ae] underline transition"
  >
    <slot />
  </NuxtLink>
</template>
