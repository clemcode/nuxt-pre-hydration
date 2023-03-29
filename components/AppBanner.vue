<script setup lang="ts">
const preferNoBanner = () => {
  localStorage.setItem('preferNoBanner', 'true')
  document.querySelector('html')?.classList.add('hide-banner')
}

if (process.server) {
  useHead({
    script: [
      {
        key: 'prehydrate-workshop-banner',
        innerHTML: `
            if (localStorage.getItem('preferNoBanner') === 'true') {
              document.querySelector('html').classList.add('hide-banner')
            }`.replace(/\s+/g, ' '),
        type: 'text/javascript'
      }
    ]
  })
}
</script>

<template>
  <div class="banner">
    <p>Pre-hydrated banner</p>
    <button @click="preferNoBanner">Don't show me again</button>
  </div>
</template>

<style>
.banner {
  background-color: #f1f1f1;
  padding: 20px;
  text-align: center;
}
.hide-banner .banner{
  display: none;
}
</style>
