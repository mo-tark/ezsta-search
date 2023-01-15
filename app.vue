<script setup>
useHead({
  title: 'EZSTA Mapping Finder',
  link: [
    {
      rel: 'icon', type: 'image/png', href: '_nuxt/assets/img/ezsta_logo.png',
    },
  ],
})
</script>

<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>

<style>
html,
body,
#__nuxt {
  height: 100vh;
  margin: 0;
  padding: 0;
}

html.dark {
  background: rgb(21, 20, 20);
  color: white;
}
</style>
