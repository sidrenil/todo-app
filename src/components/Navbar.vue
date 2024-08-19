<template>
  <nav class="main-nav">
    <router-link :to="{ name: 'Home' }">| Yapilacaklar |</router-link>
    <router-link :to="{ name: 'YapilacakEkle' }"
      >| Yapilacak Ekle |</router-link
    >
  </nav>
</template>

<script></script>

<style>
.main-nav a {
  @apply inline-block no-underline mx-2 my-10 text-neutral-400;
}
a.router-link-active {
  @apply text-base border-b-2 border-solid border-green-600;
}
</style>
