<script setup>
useHead({
  title: 'My App',
  meta: [
    { name: 'description', content: 'My amazing site.' },
    { hid: 'fb:app_id', name: 'fb:app_id', content: '12873892173892' },
    { hid: 'og:title', name: 'og:title', content: 'Blackpink Rosé shares the memory of two years back her first single album - Hourly News' },
    { hid: 'og:description', name: 'og:description', content: 'Blackpink&#8217;s Rosé recently took to social media to share a heartfelt message about her debut solo single album, &#8220;R.&#8221; The album, which was released two years ago, marked a major milestone in Rosé&#8217;s career as a musician and served as a showcase for her incredible...Continue Reading... Blackpink Rosé shares the memory of two years back her first single album' },
    { hid: 'og:image', name: 'og:image', content: 'https://thedramaclubs.com/wp-content/uploads/2023/04/olsbprosbmbm001a_1567140053.webp' },
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
