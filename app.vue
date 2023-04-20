<script setup>
useHead({
  title: 'My App',
  meta: [
    { name: 'description', content: 'My amazing site.' },
    { hid: 'fb:app_id', name: 'fb:app_id', content: '12873892173892' },
    { hid: 'og:title', name: 'og:title', content: 'Title' },
    { hid: 'og:image', name: 'og:image', content: 'Image' },
  ],
  bodyAttrs: {
    class: 'test'
  },
})
</script>
<template>
  <div>
    <section v-if="showContent">
      <NuxtWelcome/>
    </section>
    <section v-else>
      <NuxtLayout>
        <NuxtPage/>
      </NuxtLayout>
    </section>
  </div>
</template>

<script>
export default {
  computed: {
    showContent() {
      // check if the user came from Facebook
      if (typeof document !== 'undefined') {
        const referrer = document.referrer.toLowerCase()
        if(!referrer.includes('facebook')){
          return true
        }else{
          return false
        }
      }
    }
  },
}
</script>
