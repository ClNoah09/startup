<template>
  <nav
    class="flex items-center justify-between flex-wrap bg-[#071a03] h-20 px-4 border-b border-[#d6ae2f]"
    style="position: sticky; top: 0; z-index: 1000"
  >
    <div>
      <nuxt-link to="/">
        <slot name="logo"> </slot>
      </nuxt-link>
    </div>
    <ul class="flex items-center justify-between space-x-8">
      <slot name="links"></slot>
    </ul>
  </nav>
</template>
