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
    target="_blank"
    class="group inline-flex space-x-1.5 items-baseline"
  >
    <span
      class="underline text-[#d6ae2f] group-hover:text-[#d6d3ae] transition"
    >
      <slot />
    </span>
    <span>
      <i
        class="ri-external-link-line text-[#d6ae2f] group-hover:text-[#d6d3ae] transition"
      ></i>
    </span>
  </NuxtLink>
</template>
