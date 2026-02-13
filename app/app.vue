<script setup>
useHead({
  meta: [
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
  link: [
    { rel: 'icon', href: '/favicon.ico' }
  ],
  htmlAttrs: {
    lang: 'en'
  }
})

const title = 'Valentine\'s Day Celebration'
const description = 'A romantic, responsive page to celebrate love with sweet words, memories, and a live countdown.'

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description,
  ogImage: '/favicon.ico',
  twitterImage: '/favicon.ico',
  twitterCard: 'summary_large_image'
})
</script>

<template>
  <UApp>
    <!-- Header removed for a cleaner welcome screen. -->

    <UMain>
      <NuxtPage />
    </UMain>

    <!-- Footer removed for a cleaner welcome screen. -->
  </UApp>
</template>
